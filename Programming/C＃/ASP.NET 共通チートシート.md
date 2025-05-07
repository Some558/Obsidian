## 設定とスタートアップ

csharp

```csharp
// Program.cs
var builder = WebApplication.CreateBuilder(args);

// サービスの追加
builder.Services.AddControllersWithViews(); // MVC
builder.Services.AddRazorPages(); // Razor Pages
builder.Services.AddSignalR(); // SignalR
builder.Services.AddDbContext<AppDbContext>(options =>
    options.UseSqlServer(builder.Configuration.GetConnectionString("DefaultConnection")));

// DIコンテナへのサービス登録
builder.Services.AddScoped<IUserService, UserService>();
builder.Services.AddSingleton<IEmailSender, EmailSender>();
builder.Services.AddTransient<IDateTimeService, DateTimeService>();

var app = builder.Build();

// ミドルウェアの設定
if (app.Environment.IsDevelopment())
{
    app.UseDeveloperExceptionPage();
}
else
{
    app.UseExceptionHandler("/Home/Error");
    app.UseHsts();
}

app.UseHttpsRedirection();
app.UseStaticFiles();
app.UseRouting();
app.UseAuthentication();
app.UseAuthorization();

// エンドポイントの設定
app.MapControllerRoute(
    name: "default",
    pattern: "{controller=Home}/{action=Index}/{id?}");
app.MapRazorPages();

app.Run();
```

## 設定ファイル (appsettings.json)

json

```json
{
  "ConnectionStrings": {
    "DefaultConnection": "Server=localhost;Database=myDb;Trusted_Connection=True;"
  },
  "Logging": {
    "LogLevel": {
      "Default": "Information",
      "Microsoft": "Warning",
      "Microsoft.Hosting.Lifetime": "Information"
    }
  },
  "AllowedHosts": "*",
  "AppSettings": {
    "SiteTitle": "My ASP.NET App",
    "ApiKey": "your-api-key"
  }
}
```

## 設定へのアクセス

csharp

```csharp
// コンストラクタインジェクション
public class MyService
{
    private readonly IConfiguration _configuration;
    
    public MyService(IConfiguration configuration)
    {
        _configuration = configuration;
    }
    
    public void DoSomething()
    {
        // 設定値の取得
        string connectionString = _configuration.GetConnectionString("DefaultConnection");
        string apiKey = _configuration["AppSettings:ApiKey"];
        
        // 型付き設定
        var appSettings = _configuration.GetSection("AppSettings").Get<AppSettings>();
    }
}
```

## 依存性注入 (DI)

csharp

```csharp
// サービスの登録 (Program.cs)
builder.Services.AddScoped<IUserService, UserService>();

// コンストラクタインジェクション
public class UserController : Controller
{
    private readonly IUserService _userService;
    
    public UserController(IUserService userService)
    {
        _userService = userService;
    }
}
```

## Entity Framework Core

csharp

```csharp
// DbContext
public class AppDbContext : DbContext
{
    public AppDbContext(DbContextOptions<AppDbContext> options)
        : base(options)
    {
    }
    
    public DbSet<User> Users { get; set; }
    public DbSet<Product> Products { get; set; }
    
    protected override void OnModelCreating(ModelBuilder modelBuilder)
    {
        // Fluentの設定
        modelBuilder.Entity<User>()
            .HasIndex(u => u.Email)
            .IsUnique();
            
        modelBuilder.Entity<Order>()
            .HasOne(o => o.Customer)
            .WithMany(c => c.Orders)
            .HasForeignKey(o => o.CustomerId);
    }
}

// リポジトリパターン
public class UserRepository : IUserRepository
{
    private readonly AppDbContext _context;
    
    public UserRepository(AppDbContext context)
    {
        _context = context;
    }
    
    public async Task<User> GetByIdAsync(int id)
    {
        return await _context.Users.FindAsync(id);
    }
    
    public async Task<IEnumerable<User>> GetAllAsync()
    {
        return await _context.Users.ToListAsync();
    }
    
    public async Task<User> AddAsync(User user)
    {
        _context.Users.Add(user);
        await _context.SaveChangesAsync();
        return user;
    }
}
```

## Identity と認証

csharp

```csharp
// サービス登録
builder.Services.AddIdentity<ApplicationUser, IdentityRole>()
    .AddEntityFrameworkStores<AppDbContext>()
    .AddDefaultTokenProviders();

// 認証・認可ミドルウェア
app.UseAuthentication();
app.UseAuthorization();

// コントローラーでの認証
[Authorize]
public class AccountController : Controller
{
    private readonly UserManager<ApplicationUser> _userManager;
    private readonly SignInManager<ApplicationUser> _signInManager;
    
    public AccountController(
        UserManager<ApplicationUser> userManager,
        SignInManager<ApplicationUser> signInManager)
    {
        _userManager = userManager;
        _signInManager = signInManager;
    }
    
    [AllowAnonymous]
    public IActionResult Login() => View();
    
    [Authorize(Roles = "Admin")]
    public IActionResult AdminPanel() => View();
}
```

## ログとエラーハンドリング

csharp

```csharp
// ログ出力
public class ProductService
{
    private readonly ILogger<ProductService> _logger;
    
    public ProductService(ILogger<ProductService> logger)
    {
        _logger = logger;
    }
    
    public void ProcessOrder(Order order)
    {
        _logger.LogInformation("Processing order {OrderId}", order.Id);
        
        try
        {
            // 処理
        }
        catch (Exception ex)
        {
            _logger.LogError(ex, "Error processing order {OrderId}", order.Id);
            throw;
        }
    }
}

// グローバルエラーハンドリング
app.UseExceptionHandler("/Error");
```

## キャッシュ

csharp

```csharp
// メモリキャッシュ
builder.Services.AddMemoryCache();

public class ProductService
{
    private readonly IMemoryCache _cache;
    
    public ProductService(IMemoryCache cache)
    {
        _cache = cache;
    }
    
    public async Task<Product> GetProductAsync(int id)
    {
        string cacheKey = $"product_{id}";
        
        if (!_cache.TryGetValue(cacheKey, out Product product))
        {
            // キャッシュになければデータベースから取得
            product = await _dbContext.Products.FindAsync(id);
            
            // キャッシュオプション
            var cacheOptions = new MemoryCacheEntryOptions()
                .SetSlidingExpiration(TimeSpan.FromMinutes(5))
                .SetAbsoluteExpiration(TimeSpan.FromHours(1));
                
            // キャッシュに保存
            _cache.Set(cacheKey, product, cacheOptions);
        }
        
        return product;
    }
}
```

## HttpClient

csharp

```csharp
// サービス登録
builder.Services.AddHttpClient("github", client =>
{
    client.BaseAddress = new Uri("https://api.github.com/");
    client.DefaultRequestHeaders.Add("Accept", "application/vnd.github.v3+json");
    client.DefaultRequestHeaders.Add("User-Agent", "HttpClientFactory-Sample");
});

// 使用例
public class GitHubService
{
    private readonly IHttpClientFactory _clientFactory;
    
    public GitHubService(IHttpClientFactory clientFactory)
    {
        _clientFactory = clientFactory;
    }
    
    public async Task<IEnumerable<RepoItem>> GetReposAsync()
    {
        var client = _clientFactory.CreateClient("github");
        var response = await client.GetAsync("/repos/dotnet/aspnetcore");
        
        if (response.IsSuccessStatusCode)
        {
            return await response.Content.ReadFromJsonAsync<IEnumerable<RepoItem>>();
        }
        
        return Array.Empty<RepoItem>();
    }
}
```

## SignalR

csharp

```csharp
// Hub定義
public class ChatHub : Hub
{
    public async Task SendMessage(string user, string message)
    {
        await Clients.All.SendAsync("ReceiveMessage", user, message);
    }
}

// サービス登録
builder.Services.AddSignalR();

// エンドポイント設定
app.MapHub<ChatHub>("/chatHub");

// クライアント側
<script>
    const connection = new signalR.HubConnectionBuilder()
        .withUrl("/chatHub")
        .build();
        
    connection.on("ReceiveMessage", (user, message) => {
        const msg = `${user}: ${message}`;
        const li = document.createElement("li");
        li.textContent = msg;
        document.getElementById("messagesList").appendChild(li);
    });
    
    connection.start().catch(err => console.error(err));
    
    document.getElementById("sendButton").addEventListener("click", event => {
        const user = document.getElementById("userInput").value;
        const message = document.getElementById("messageInput").value;
        connection.invoke("SendMessage", user, message).catch(err => console.error(err));
        event.preventDefault();
    });
</script>
```

## Middleware カスタム作成

csharp

```csharp
public class RequestLoggingMiddleware
{
    private readonly RequestDelegate _next;
    private readonly ILogger _logger;

    public RequestLoggingMiddleware(RequestDelegate next, ILogger<RequestLoggingMiddleware> logger)
    {
        _next = next;
        _logger = logger;
    }

    public async Task InvokeAsync(HttpContext context)
    {
        _logger.LogInformation($"Request: {context.Request.Path}");
        
        // 次のミドルウェアを呼び出し
        await _next(context);
        
        _logger.LogInformation($"Response Status: {context.Response.StatusCode}");
    }
}

// 拡張メソッド
public static class RequestLoggingMiddlewareExtensions
{
    public static IApplicationBuilder UseRequestLogging(this IApplicationBuilder builder)
    {
        return builder.UseMiddleware<RequestLoggingMiddleware>();
    }
}

// 使用
app.UseRequestLogging();
```

## ファイルアップロード

csharp

```csharp
public async Task<IActionResult> Upload(IFormFile file)
{
    if (file != null && file.Length > 0)
    {
        var filePath = Path.Combine(
            Directory.GetCurrentDirectory(), "wwwroot/uploads",
            Path.GetRandomFileName() + Path.GetExtension(file.FileName));
            
        using (var stream = new FileStream(filePath, FileMode.Create))
        {
            await file.CopyToAsync(stream);
        }
        
        return Ok(new { filePath });
    }
    
    return BadRequest("No file was uploaded");
}
```

## バックグラウンド処理

csharp

```csharp
// バックグラウンドサービス登録
builder.Services.AddHostedService<QueuedHostedService>();

// ホステッドサービス実装
public class QueuedHostedService : BackgroundService
{
    private readonly ILogger<QueuedHostedService> _logger;
    private readonly IBackgroundTaskQueue _taskQueue;

    public QueuedHostedService(
        IBackgroundTaskQueue taskQueue,
        ILogger<QueuedHostedService> logger)
    {
        _taskQueue = taskQueue;
        _logger = logger;
    }

    protected override async Task ExecuteAsync(CancellationToken stoppingToken)
    {
        _logger.LogInformation("Queued Hosted Service is starting.");

        while (!stoppingToken.IsCancellationRequested)
        {
            var workItem = await _taskQueue.DequeueAsync(stoppingToken);

            try
            {
                await workItem(stoppingToken);
            }
            catch (Exception ex)
            {
                _logger.LogError(ex, "Error occurred executing {WorkItem}.", nameof(workItem));
            }
        }

        _logger.LogInformation("Queued Hosted Service is stopping.");
    }
}
```

## 主要な名前空間と参照先

|名前空間|主な用途|
|---|---|
|Microsoft.AspNetCore.Mvc|MVC, API|
|Microsoft.AspNetCore.Razor|Razor構文|
|Microsoft.AspNetCore.Identity|認証・認可|
|Microsoft.EntityFrameworkCore|データアクセス|
|Microsoft.Extensions.Configuration|設定|
|Microsoft.Extensions.DependencyInjection|DI|
|Microsoft.Extensions.Logging|ログ|
|Microsoft.Extensions.Caching|キャッシュ|
|Microsoft.AspNetCore.SignalR|リアルタイム通信|
|Microsoft.AspNetCore.Authentication|認証|
|Microsoft.AspNetCore.Authorization|認可|
|Microsoft.AspNetCore.Http|HTTPコンテキスト|
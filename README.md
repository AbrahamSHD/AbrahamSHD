<div id="user-content-toc">
  <ul align="center">
    <summary><h1 style="display: inline-block">Hey 👋 Soy AbrahamHC</h1></summary>
  </ul>
</div>
<p>

- ☁️ Tengo gran interés en el desarrollo backend. estoy aprendiendo y creando nuevos prouectos con Nest js.

- 🔭 Actualmente estoy trabajando con Nest js, Typescript y PostgreSQL/MongoDb.

- 📫 No dudes en comunicarte conmigo hernandez.c.abraham.00@gmail.com

- <a href="https://porfolio-ahc.netlify.app/" target="_blank" rel="noopener">💼 Portfolio</a>
</p>
<br>

<div id="user-content-toc">
  <ul align="center">
    <summary><h2 style="display: inline-block">Tecnologías y herramientas que conozco 👨🏻‍💻</h2></summary>
  </ul>
</div>

<p align="center">
  <a href="https://skillicons.dev">
    <img src="https://skillicons.dev/icons?i=html,css,tailwind,js,ts,vite"><br><br>
    <img src="https://skillicons.dev/icons?i=nodejs,express,nest,postman,npm"><br><br>
    <img src="https://skillicons.dev/icons?i=mongodb,postgresql,prisma"><br><br>
    <img src="https://skillicons.dev/icons?i=git,github,ubuntu,powershell,vscode&perline=14" />
  </a>
</p>


using DotNetEnv;

var builder = WebApplication.CreateBuilder(args);

// Cargar variables de entorno desde .env
DotNetEnv.Env.Load();

// Registrar el valor de la variable FILE_PATH como un servicio
builder.Services.AddSingleton(provider =>
{
    string filePath = Environment.GetEnvironmentVariable("FILE_PATH");
    if (string.IsNullOrEmpty(filePath))
    {
        throw new Exception("La variable FILE_PATH no está definida en el archivo .env.");
    }
    return filePath;
});

// Registrar servicios como ExcelReader
builder.Services.AddSingleton<ExcelReader>();
builder.Services.AddScoped<MeetingService>();

var app = builder.Build();

app.MapGet("/", (MeetingService meetingService) =>
{
    return meetingService.GetAllMeetings();
});

app.Run();
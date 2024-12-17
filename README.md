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


```

using Application.Services;
using Infrastructure.Data;
using Microsoft.Extensions.Configuration;
using Microsoft.OpenApi.Models;

var builder = WebApplication.CreateBuilder(args);

// 1. Cargar las variables de entorno del archivo .env
builder.Configuration.AddEnvironmentVariables(); // Cargar las variables desde .env si está configurado

// 2. Configurar el servicio para acceder a las variables de entorno
builder.Services.AddSingleton<IConfiguration>(builder.Configuration);

// 3. Agregar servicios al contenedor de dependencias
builder.Services.AddControllers();

// Registrar los servicios de aplicación
builder.Services.AddScoped<ExcelReader>();
builder.Services.AddScoped<MeetingService>();

// Configuración de Swagger para la API
builder.Services.AddEndpointsApiExplorer();
builder.Services.AddSwaggerGen(c =>
{
    c.SwaggerDoc("v1", new OpenApiInfo { Title = "School API", Version = "v1" });
});

var app = builder.Build();

// Configurar el middleware
if (app.Environment.IsDevelopment())
{
    app.UseSwagger();
    app.UseSwaggerUI(c => c.SwaggerEndpoint("/swagger/v1/swagger.json", "School API v1"));
}

app.UseHttpsRedirection();
app.UseAuthorization();
app.MapControllers();

// Iniciar la aplicación
app.Run();

```
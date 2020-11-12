# Nuget Packages into API project:
Swashbuckle.AspNetCore.Swagger
Swashbuckle.AspNetCore.SwaggerGen
Swashbuckle.AspNetCore.Swagger

# Startup.cs

```csharp

    //At the end of configure services

            services.AddSwaggerGen(c =>
            {
                c.SwaggerDoc("v1", new OpenApiInfo { Title = "Players API", Version = "v1" });
                var xmlFile = $"{Assembly.GetExecutingAssembly().GetName().Name}.xml";
                var xmlPath = Path.Combine(AppContext.BaseDirectory, xmlFile);
                c.IncludeXmlComments(xmlPath);
            });

    //Above use MVC but below use Endpoints in Configure method

    app.UseSwagger();
    app.UseSwaggerUI(c =>
    {
        c.SwaggerEndpoint("../swagger/v1/swagger.json", "Players API");
        c.RoutePrefix = string.Empty;
    });

```
# .csproj

<PropertyGroup>
    <GenerateDocumentationFile>true</GenerateDocumentationFile>
</PropertyGroup>

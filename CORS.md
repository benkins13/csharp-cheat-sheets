# Adding CORS to an API

## Startup

```csharp
public void ConfigureServices(IServiceCollection services)
        {

            services.AddCors(c =>
            {
                c.AddPolicy("AllowOrigin", options => options.AllowAnyOrigin().AllowAnyHeader().AllowAnyMethod()); //Make sure this is at the top of the method
            });

            services.AddControllers();

            services.AddScoped<IService, Service>();
        }

        public void Configure(IApplicationBuilder app, IWebHostEnvironment env)
        {
            if (env.IsDevelopment())
            {
                app.UseDeveloperExceptionPage();
            }


            app.UseHttpsRedirection();

            app.UseRouting();

            app.UseAuthorization();

            app.UseCors(options => options.AllowAnyOrigin().AllowAnyHeader().AllowAnyMethod()); //Make sure this is above UseEndpoints and below UseAuthorization

            app.UseEndpoints(endpoints =>
            {
                endpoints.MapControllers();
            });
        }
```

## API Controller

```csharp
using Microsoft.AspNetCore.Cors;

namespace Brenda.Controllers
{
    [Route("api/[controller]")]
    [EnableCors("AllowOrigin")] //Add this to the top of every controller that you want the CORS policy on
    [ApiController]
```

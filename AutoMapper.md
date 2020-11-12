# Adding AutoMapper to a project

## Startup

```csharp
public void ConfigureServices(IServiceCollection services)
        {
            var mappingConfig = new MapperConfiguration(mc =>   //
            {                                                   //
                mc.AddProfile(new MappingProfile());            // This adds the mapping profile class -- See below class
            });                                                 //
                                                                //
            var mapper = mappingConfig.CreateMapper();          //
                                                                //
            services.AddSingleton(mapper);                      // <-- Important

            services.AddControllers();

            services.AddScoped<IService, Service>();
        }

```

## MappingProfile

```csharp
using AutoMapper;
using Brenda.DataLayer.Models;
using Brenda.ServiceLayer.Models;

namespace Brenda
{
    public class MappingProfile : Profile                               // Inherit Profile
    {
        public MappingProfile()
        {
            CreateMap<Skill, SkillModel>().ReverseMap();                //
            CreateMap<SkillLevel, SkillLevelModel>().ReverseMap();      // Add mappings here
            CreateMap<User, UserModel>().ReverseMap();                  // Add .ReverseMap() to allow you to map both ways
            CreateMap<Level, LevelModel>().ReverseMap();                //
        }
    }
}

```

## Using the mapper you've made

```csharp
using AutoMapper;

namespace Brenda.ServiceLayer
{
    public class Service : IService
    {
        private readonly IMapper _mapper;

        public Service(IMapper mapper)
        {
            this._mapper = mapper;          //Injecting the mapper
        }
```

## Mapping a model

```csharp
var skillModel = _mapper.Map<Skill, SkillModel>(skill);
//This maps the variable "skill" which is a Skill, and maps it to a Skill Model ---> The result is then assigned to skillModel
```

# serilog-demo-app
serilog-demo-app
1. dotnet new webapi -o "myapi"
2. dotnet add package Serilog.AspNetCore
3. dotnet add package Serilog.Sinks.Console
4. dotnet add package Serilog.Sinks.File

5. AppSettings.json changes

{
  "Serilog": {
    "MinimumLevel":"Information",
    "Override":{"Microsoft.AspNetCore":"Warning"},
    "WriteTo":[
      {"Name":"Console"},
      {"Name": "File",
        "Args": {
          "path": "logs\\AppLogs.log",
          "formatter":"Serilog.Formatting.Json.JsonFormatter, Serilog"
        }
      }
    ]
    
  },
  "AllowedHosts": "*"
}

6. Program.cs 

using Serilog;
   public static IHostBuilder CreateHostBuilder(string[] args) =>
            Host.CreateDefaultBuilder(args)
            .UseSerilog()
                .ConfigureWebHostDefaults(webBuilder =>
                {
                    webBuilder.UseStartup<Startup>();
                });
    }
	
7. Startup.cs
using Serilog


        public Startup(IConfiguration configuration)
        {
            Configuration = configuration;
            Log.Logger = new LoggerConfiguration().ReadFrom.Configuration(configuration).CreateLogger();
        }
		
8.   controller add 
 _logger.LogInformation($"This is Get Method of Weather Forecast. {Summaries[0]}");
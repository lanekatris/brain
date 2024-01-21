---
title: Serilog log level in GCP
date: 2024-01-19
---

```
public class GcpLogLevelEnricher : ILogEventEnricher
{
    private static string TranslateSeverity(LogEventLevel level) => level switch {
        LogEventLevel.Verbose => "DEBUG",
        LogEventLevel.Debug => "DEBUG",
        LogEventLevel.Information => "INFO",
        LogEventLevel.Warning => "WARNING",
        LogEventLevel.Error => "ERROR",
        LogEventLevel.Fatal => "CRITICAL",
        _ => "DEFAULT"
    };
	
    public void Enrich(LogEvent logEvent, ILogEventPropertyFactory propertyFactory)
    {
	logEvent.AddOrUpdateProperty(propertyFactory.CreateProperty("severity", TranslateSeverity(logEvent.Level)));
    }
}
```
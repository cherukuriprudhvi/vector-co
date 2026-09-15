

$setup = $can.Configuration.OnlineSetup

"Trace:   " + ($null -ne $setup.TraceCollection)
"Graphics:" + ($null -ne $setup.GraphicCollection)
"Data:    " + ($null -ne $setup.DataCollection)
"Logging: " + ($null -ne $setup.LoggingCollection)
"Send:    " + ($null -ne $setup.SendNodes)
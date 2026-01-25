# Go

Implementación server-to-server con Go.

## Código de Ejemplo

```go
package main

import (
    "bytes"
    "encoding/json"
    "net/http"
    "time"
)

type Event struct {
    EventType  string                 `json:"event_type"`
    Event      string                 `json:"event"`
    UserID     string                 `json:"user_id"`
    Timestamp  string                 `json:"timestamp"`
    Properties map[string]interface{} `json:"properties"`
}

func trackEvent(eventName, userID string, properties map[string]interface{}) error {
    event := Event{
        EventType:  "track",
        Event:      eventName,
        UserID:     userID,
        Timestamp:  time.Now().UTC().Format(time.RFC3339),
        Properties: properties,
    }
    
    jsonData, _ := json.Marshal(event)
    
    req, _ := http.NewRequest("POST", 
        "https://tracking.midas.com/api/v1/s2s/event", 
        bytes.NewBuffer(jsonData))
    
    req.Header.Set("Content-Type", "application/json")
    req.Header.Set("X-Auth-Token", "s2s.TU_SERVER_SECRET.AQUI")
    
    client := &http.Client{}
    resp, err := client.Do(req)
    if err != nil {
        return err
    }
    defer resp.Body.Close()
    
    return nil
}

func main() {
    properties := map[string]interface{}{
        "feature": "export_data",
        "format": "csv",
    }
    
    trackEvent("feature_used", "user_123", properties)
}
```

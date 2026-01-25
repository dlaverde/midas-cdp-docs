# PHP

Implementación server-to-server con PHP.

## Código de Ejemplo

```php
<?php

function trackEvent($eventName, $userId, $properties = []) {
    $url = 'https://tracking.midas.com/api/v1/s2s/event';
    
    $data = [
        'event_type' => 'track',
        'event' => $eventName,
        'user_id' => $userId,
        'timestamp' => gmdate('Y-m-d\TH:i:s\Z'),
        'properties' => $properties
    ];
    
    $ch = curl_init($url);
    curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
    curl_setopt($ch, CURLOPT_POST, true);
    curl_setopt($ch, CURLOPT_POSTFIELDS, json_encode($data));
    curl_setopt($ch, CURLOPT_HTTPHEADER, [
        'Content-Type: application/json',
        'X-Auth-Token: s2s.TU_SERVER_SECRET.AQUI'
    ]);
    
    $response = curl_exec($ch);
    curl_close($ch);
    
    return json_decode($response, true);
}

// Uso
trackEvent('payment_failed', 'user_123', [
    'error_code' => 'insufficient_funds',
    'amount' => 99.99
]);
?>
```

## Con Laravel

```php
Route::post('/signup', function (Request $request) {
    trackEvent('user_signup', $request->user()->id, [
        'email' => $request->email
    ]);
    
    return response()->json(['success' => true]);
});
```

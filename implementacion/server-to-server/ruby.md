# Ruby

Implementación server-to-server con Ruby.

## Código de Ejemplo

```ruby
require 'net/http'
require 'json'
require 'uri'

def track_event(event_name, user_id, properties = {})
  uri = URI('https://tracking.midas.com/api/v1/s2s/event')
  
  payload = {
    event_type: 'track',
    event: event_name,
    user_id: user_id,
    timestamp: Time.now.utc.iso8601,
    properties: properties
  }
  
  http = Net::HTTP.new(uri.host, uri.port)
  http.use_ssl = true
  
  request = Net::HTTP::Post.new(uri.path)
  request['Content-Type'] = 'application/json'
  request['X-Auth-Token'] = 's2s.TU_SERVER_SECRET.AQUI'
  request.body = payload.to_json
  
  response = http.request(request)
  JSON.parse(response.body)
end

# Uso
track_event('trial_started', 'user_123', {
  trial_length: 14,
  plan: 'enterprise'
})
```

## Con Rails

```ruby
class SignupsController < ApplicationController
  def create
    track_event('user_signup', @user.id, {
      email: params[:email]
    })
    
    render json: { success: true }
  end
end
```

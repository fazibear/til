# Today I Learned

<details>
<summary>09.05.2019 Phoenix PubSub</summary>
If you need a pubsub, to connect LiveViews for example just use YourAppWeb.Endpoint.

```elixir
YourAppWeb.Endpoint.subscribe("topic")
```

```elixir
YourAppWeb.Endpoint.broadcast("topic", "event", %{data: "data"})
```

```elixir
def handle_info(%{event: "event", topic: "topic", payload: payload}) do
  # Do whatever you want
end
```
</details>

<details>
<summary>13.05.2019 Discover SSH service using mDNS</summary>
To nake service discoverable we need following services registered:

```elixir
# create domain for an ip
%Mdns.Server.Service{domain: "somedomain.local", data: :ip, ttl: 450, type: :a},

# make device discoverable at all
Mdns.Server.add_service(%Mdns.Server.Service{domain: "_services._dns-sd._udp.local",data: "SOME NAME._services._dns-sd._udp.local",ttl: 4500,type: :ptr})

# register ssh service
Mdns.Server.add_service(%Mdns.Server.Service{domain: "_ssh._tcp.local",data: "SOME NAME._ssh._tcp.local",ttl: 4500,type: :ptr})

# point service to our domain and port (22)
Mdns.Server.add_service(%Mdns.Server.Service{domain: "SOME NAME._ssh._tcp.local",data: {0,0,22, 'domain.local'},ttl: 4500,type: :srv})

# empty txt service (some tools expext that)
Mdns.Server.add_service(%Mdns.Server.Service{domain: "SOME NAME._ssh._tcp.local",data: [],ttl: 4500,type: :txt})
```
</details>

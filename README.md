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
To make service discoverable we need following services registered:

```elixir
[
  # create domain for an ip
  %Mdns.Server.Service{domain: "somedomain.local", data: :ip, ttl: 450, type: :a},

  # make service discoverable
  %Mdns.Server.Service{domain: "_services._dns-sd._udp.local",data: "_ssh._tcp.local",ttl: 4500, type: :ptr},

  # register ssh service
  %Mdns.Server.Service{domain: "_ssh._tcp.local",data: "SOME NAME._ssh._tcp.local",ttl: 4500, type: :ptr},

  # point service to our domain and port (22)
  %Mdns.Server.Service{domain: "SOME NAME._ssh._tcp.local",data: {0,0,22, 'somedomain.local'},ttl: 4500,type: :srv},

  # empty txt service (some tools expext that)
  %Mdns.Server.Service{domain: "SOME NAME._ssh._tcp.local",data: [],ttl: 4500,type: :txt})
] |> Enum.each(&Mdns.Server.add_service/1)
```
</details>

<details>
<summary>16.05.2019 Get state of GenServer</summary>
To get state of any process in erlang/elixir use `:sys.get_state/1`


By name:
```elixir
:sys.get_state(MyGenServer)
```

By pid:
```elixir
:sys.get_state(pid)
```
</details>

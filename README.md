```

# Criar os networks namespaces
# Hosts
ip netns add h1
ip netns add h2
ip netns add h3
ip netns add h4
ip netns add h5
ip netns add h6
ip netns add h7
ip netns add h8

# Routers
ip netns add r1
ip netns add r2
ip netns add r3
ip netns add r4
ip netns add r5
ip netns add r6
ip netns add r7

# Cria os links e as interfaces virtuais
ip link add h1-0 type veth peer name h1-1
ip link add h2-0 type veth peer name h2-1
ip link add h3-0 type veth peer name h3-1
ip link add h4-0 type veth peer name h4-1
ip link add h5-0 type veth peer name h5-1
ip link add h6-0 type veth peer name h6-1
ip link add h7-0 type veth peer name h7-1
ip link add h8-0 type veth peer name h8-1

# Move as interfaces para os namespaces
ip link set h1-0 netns h1
ip link set h2-0 netns h2
ip link set h3-0 netns h3
ip link set h4-0 netns h4
ip link set h5-0 netns h5
ip link set h6-0 netns h6
ip link set h7-0 netns h7
ip link set h8-0 netns h8

# Configura os endereços IPs e ativa as interfaces de rede
ip netns exec h1 ifconfig h1-0 10.0.1.1 netmask 255.255.255.0 up
ip netns exec h1 ifconfig lo up
ip netns exec h2 ifconfig h2-0 10.0.1.2 netmask 255.255.255.0 up
ip netns exec h2 ifconfig lo up
ip netns exec h3 ifconfig h3-0 10.0.1.3 netmask 255.255.255.0 up
ip netns exec h3 ifconfig lo up
ip netns exec h4 ifconfig h4-0 10.0.1.4 netmask 255.255.255.0 up
ip netns exec h4 ifconfig lo up
ip netns exec h5 ifconfig h5-0 10.0.1.5 netmask 255.255.255.0 up
ip netns exec h5 ifconfig lo up
ip netns exec h6 ifconfig h6-0 10.0.1.6 netmask 255.255.255.0 up
ip netns exec h6 ifconfig lo up
ip netns exec h7 ifconfig h7-0 10.0.1.7 netmask 255.255.255.0 up
ip netns exec h7 ifconfig lo up
ip netns exec h8 ifconfig h8-0 10.0.1.8 netmask 255.255.255.0 up
ip netns exec h8 ifconfig lo up 


# para cada roteador, executar um codigo de dar echo no /etc/proc/

# Cria ponte transparente
brctl addbr br0
ifconfig br0 up

# Adiciona interfaces à ponte
brctl addif br0 h1-1
brctl addif br0 h2-1
brctl addif br0 h3-1

# Ativa as interfaces da ponte
ifconfig h1-1 up
ifconfig h2-1 up
ifconfig h3-1 up

```
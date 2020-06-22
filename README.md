Various automation goodies

* net-ssh

A poor man VPN. Use it to join a remote network via SSH. Just run

net-ssh --server=root@12.34.56.78:20022 --net=10.1.1.0/24 --tun-spec=2:5 --tun-addr=10.190.190.1:2

This will ssh as root (required to patch iptables and configure a tunnel) into server 12.34.56.78:20022
create tun2 interface on the client and tun5 on the server, assign IP 10.190.190.1 to tun2, assign 10.190.190.2
to tun5, configure routing on the client and iptables on the sever in order to access local server
network 10.1.1.0/24 from the client machine.

I wrote it as a personal replacement for sshuttle which is great in many ways except speed.
My script doesn't implement packet routing/forwarding but rather delegates this to iptables to handle it which, in
my personal experience, results into 2-5 times faster
speeds, depending on the actual bandwidth between client and server.

I only suggest using this script over sshuttle only if:
1) you have remote root access via ssh and
2) you need a faster channel

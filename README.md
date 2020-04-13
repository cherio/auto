Various automation goodies

* net-ssh

A poor man VPN. Use it to join a remote network via SSH. Just run

net-ssh --server=root@12.34.56.78:20022 --net=10.1.1.0/24 --tun-spec=2:5 --tun-addr=10.190.190.1:2

This will ssh as root (required to patch iptables and configure a tunnel) into server 12.34.56.78:20022
create tun2 interface on the client and tun5 on the server, assign IP 10.190.190.1 to tun2, assign 10.190.190.2
to tun5, configure routing on the client and iptables on the sever in order to access local server
network 10.1.1.0/24 from the client machine.

I wrote it as a replacement for sshuttle. I love sshuttle! It is better than my script in many ways.
Except for speed. My script delegates packet forwarding to iptables which is 2-5 times faster (in my personal
experience), depending on the actual bandwidth between client and server. sshuttle doesn't require connecting
as root. It performs it's own packet forwarding/routing.

I suggest use my script and not sshuttle only if:
1) you can ssh as root and
2) you need a faster channel

Otherwise I recommend using sshuttle.

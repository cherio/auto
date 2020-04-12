Various automation goodies

* net-ssh

A poor man VPN. Use it to join a remote network via SSH. Just run

net-ssh --server=root@12.34.56.78:20022 --net=10.1.1.0/24 --tun-spec=2:5 --tun-addr=10.190.190.1:2

This will ssh as root (required to patch iptables and configure a tunnel) into server 12.34.56.78:20022
create tun2 interface on the client and tun5 on the server, assign IP 10.190.190.1 to tun2, assign 10.190.190.2
to tun5, configure routing on the client and iptables on the sever in order to access local server
network 10.1.1.0/24 from the client machine.

I wrote it as a replacement for sshuttle. I love sshuttle! It is better than my script in many ways.
Except for speed. This way to join a remote network is 2-5 times faster, depending on the bandwidth between
client and server. sshuttle performs its own packet routing. It doesn't require connection as root.

I suggest only use my script and not sshuttle if:
1) you can ssh as root and
2) you need better communication speed

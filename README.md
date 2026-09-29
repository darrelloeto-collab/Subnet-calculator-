# Subnet-calculator-
import ipaddress


def subnet_calculator():
    print(" IPv4 SUBNET CALCULATOR ")

    ip_address = input("Enter IP address (example: 192.168.1.0): ")
    prefix = input("Enter CIDR prefix (example: /26): ")

    try:
        if not prefix.startswith("/"):
            prefix = "/" + prefix

        network = ipaddress.ip_network(
            ip_address + prefix,
            strict=False
        )

        print("\n RESULTS ")
        print("IP Address:       ", ip_address)
        print("CIDR Prefix:      ", network.prefixlen)
        print("Subnet Mask:      ", network.netmask)
        print("Network Address:  ", network.network_address)
        print("Broadcast Address:", network.broadcast_address)

        hosts = list(network.hosts())

        if len(hosts) > 0:
            print("First Host:       ", hosts[0])
            print("Last Host:        ", hosts[-1])
            print("Usable Hosts:     ", len(hosts))
        else:
            print("First Host:        None")
            print("Last Host:         None")
            print("Usable Hosts:      0")

    except ValueError:
        print("\nInvalid IP address or CIDR prefix.")
        print("Example: 192.168.1.0 /26")


subnet_calculator()

# Controlled Access
# Points: 50
# We've been asked to help a certificate authority figure out what a device they found plugged into their network was doing. 
# They were able to dump the firmware and would like to know if it allowed the attacker to connect to any devices that their firewall (which blocks inbound SSH) would have stopped. Their internal domain uses 'digisigner.local' for DNS host names. 
# The flag is the hostname of the internal host that the hacker targeted (i.e. ACI{[local hostname targeted]}).

### [Solution]
    Using binwalk to extract the information from the .bin (binwalk firmware.bin -e)
    Navigating into the file you can see the file system for the hacking device
    Listed on the website is the default configs for the device and under /root/payload/payload.sh the folliwing was found
    #!/bin/bash
    #
    # Title:         Secure Shark Jacker
    # Author:        Mr. Robot
    # Version:       13.37
    #
    INTERNAL_HOST=rootca.digisigner.local
    INTERNAL_PORT=22

    This is our answer
    Flag:{rootca.digisigner.local}

# mikrotik script for two providers
#netwatch 8.8.4.4
#when UP:
/ip route disable [find comment="ISP-2"]
/ip route enable [find comment="ISP-1"]
:foreach i in=[/ip firewall connection find protocol~"tcp"] do={ /ip firewall connection remove $i }
:foreach i in=[/ip firewall connection find protocol~"udp"] do={ /ip firewall connection remove $i }
log warning ("ISP-1 IS UP")

#when DOWN:
/ip route disable [find comment="ISP-1"]
/ip route enable [find comment="ISP-2"]
:foreach i in=[/ip firewall connection find protocol~"tcp"] do={ /ip firewall connection remove $i }
:foreach i in=[/ip firewall connection find protocol~"udp"] do={ /ip firewall connection remove $i }
log warning ("ISP-1 IS DOWN")

#do some other settings from this instruction
#https://настройка-микротик.укр/nastrojka-neskolkih-provajderov-na-mikrotik-balansirovka-i-avtopereklyuchenie/

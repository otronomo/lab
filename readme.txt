README


snmpwalk -On -v2c -c public 10.20.20.100 1.3.6.1.2.1.4.24.3.0


def inventory_ios_num_routes(info):
   # Debug: lets see how the data we get looks like
#   print info
   for routes in info:
       yield info[0], None

def check_ios_num_routes(item, params, info):
   return (3, "UNKNOWN - not yet implemented")

check_info["ios_num_routes"] = {
    "check_function"        : check_ios_num_routes,
    "inventory_function"    : inventory_ios_num_routes,
    "service_description"   : "Num routes %s",
    "snmp_info"             : ( ".1.3.6.1.2.1.4.24.3", ["0"] )
}

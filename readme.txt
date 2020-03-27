README

All routes
snmpwalk -On -v2c -c public 10.20.20.100 1.3.6.1.2.1.4.24.3.0

EIGRP routes:
snmpwalk -On -v2C -c ekH6bN5# 10.20.20.100 1.3.6.1.4.1.9.9.449.1.2.1.1.19

def inventory_ios_num_routes(info):
   for routes in info:
       yield routes[0], None


def check_ios_num_routes(item, params, info):
   for routes in info:
       routes = str(routes[0])
       perfdata = [ ( "rutas", routes, 22, 30 ) ]
       return (0, "Numero rutas: " + routes, perfdata)


check_info["ios_num_routes"] = {
    "check_function"        : check_ios_num_routes,
    "inventory_function"    : inventory_ios_num_routes,
    "service_description"   : "Num routes ",
    "snmp_info"             : ( ".1.3.6.1.2.1.4.24.3", ["0"] ),
    'has_perfdata'          : True,
}

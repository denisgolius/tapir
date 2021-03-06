# TAPIR #

**Tapir** is an open source solution for troubleshooting and real-time monitoring of VoIP-network based systems. 
It has an easy scalable architecture, fast and clear WEB UI and, as a result, provides the best way to analyze end-to-end 
call correlation. 

**Tapir** reduces operational costs, prevents voice fraud, increases system availability 
time.

### ###

![](https://cloud.githubusercontent.com/assets/1871737/23656420/b089fe5e-034a-11e7-8244-4a2a7594ddd3.gif)

### Tapir includes four modules: ###

1. **Tapir Captain** is a network sniffer for traffic capturing and parsing.
2. **Tapir Salto** aggregates traffic from **Captain** and stores it to DB-engine.
3. **Tapir Twig** provides REST API for **Hoof** to get data from the database.
4. **Tapir Hoof** is a convenient and easy web-based user interface to search and display call data.

**Captain** can capture data directly from the network interface (UDP/TCP/encapsulated IP2IP), from a single PCAP file or check a directory for new incoming data files to process.

**Salto** receives parsed data from **Captain**, validates its structure and stores extracted data in the database. Since March 2017 we can process HEPv3 packets too. The **Salto** can be easily scaled to achieve the desired performance. 

**Twig** offers REST API for user interface queries and presents statistical data.

**Hoof** includes dashboard with widgets and SIP search page. Each call can be displayed as a graphic callflow and a raw message view. There's an option for pcap-file export as well. 

**Tapir** modules are powered by high-performance Java code. It uses fast and reliable MongoDB database for the signaling data. So scaling of any module is just clear. There's also Redis cache to store and access statistical metrics for instant operation on them. 
**Tapir Hoof** is based on ReactJS which provides a simple way to create custom web interface.

**Tapir** solution is to be used by telecom operators and service providers, who aims the excellent service quality. **Tapir** provides fast search 
and significant time savings in problems solving for trunk and access connections. 
**Tapir** minimizes time to detect and resolve of network issues and customer problems. 

### Tapir architecture ###

![](https://cloud.githubusercontent.com/assets/16978841/23796440/608eb4f0-05b4-11e7-92f7-93138579694b.png)

### Installation ###

To deploy **Tapir** modules, follow build and installation instructions: [Captain](https://github.com/sip3io/tapir/tree/master/captain "Captain Installation guide"), 
[Salto](https://github.com/sip3io/tapir/tree/master/salto "Salto Installation guide"), [Twig](https://github.com/sip3io/tapir/tree/master/twig "Twig Installation guide"), 
[Hoof](https://github.com/sip3io/tapir-hoof "Hoof Installation guide").

At the moment we've described build and installation process only for Linux users. Let us know if you want to deploy Tapir on OS Windows.

#### Docker friendly ####

The Docker installation procedure works well for both sip3io/tapir and sip3io/tapir-hoof. 

1. Pull form github 
	
	cd ~
	git clone https://github.com/sip3io/tapir.git
	cd ./tapir/package/docker
	docker-compose up -d

2. Open web browser and go to http://dockerhostname

3. For process tcpdump, you can put pcap files to /tmp directory in docker host.
	
	e.g. # tcpdump -i any -s 0 -nnn -w /tmp/tapir_capture-file_ -C 50 -W 20 "port 5060"

4. Directory of configs:
	
	docker volume inspect docker_tapir-configs | grep "Mountpoint"| tr -d \",: | awk '{print $2}' 
	
	e.g.: /var/lib/docker/volumes/docker_tapir-configs/_data

5. Directory of logs:
	
	docker volume inspect docker_tapir-logs | grep "Mountpoint" | tr -d \",: | awk '{print $2}' 
	
	e.g.: /var/lib/docker/volumes/docker_tapir-logs/_data


### Versions ###

**Tapir** is distributed in two different versions: Community and Enterprise. Summary comparison table is given below.

| Functionality              | Community | Enterprise |
|----------------------------|-----------|------------|
| Unlimited sessions         | Yes       | No         |
| Сall-legs join             | Yes       | Yes        |
| Authorization/Roles        | No        | Yes        |
| Statistical metrics        | Limited   | Full       |
| SIP KPI                    | Limited   | Full       |
| Source SPAN                | Yes       | Yes        |
| Source pcap/pcap.gz files  | Yes       | Yes        |
| SIP-I support              | No        | Yes        |
| Scalability                | Full      | Full       |
| Extended search            | No        | Yes        |
| Technical assistance       | No        | Yes        |
| Quality dashboards         | Limited   | Full       |

**SIP KPI** table of Community and Enterprise metrics is shown below. 

| Metric                                     | Community | Enterprise |
|--------------------------------------------|-----------|------------|
| MPS - messages per second                  | Yes       | Yes        |
| TPS - transactions per second              | Yes       | Yes        |
| CPS - calls per second                     | Yes       | Yes        |
| RPS - registers per second                 | Yes       | Yes        |
| RPS - registers per second                 | Yes       | Yes        |
| 4XX - error responses with 4xx statuses    | Yes       | Yes        |
| 5XX - error responses with 5xx statuses    | Yes       | Yes        |
| 6XX - error responses with 6xx statuses    | Yes       | Yes        |
| ASR - answer seizure ratio                 | Yes       | Yes        |
| ACD - average call duration                | No        | Yes        |
| ACST - average call setup time             | No        | Yes        |
| ACDT - average call disconnection time     | No        | Yes        |
| RRD - registration request delay           | No        | Yes        |


### License & Contributing ###

This project is available under the Apache License 2.0. We welcome any contributions submitted as pull requests, 
wiki edits or issues under the terms of the project's license.

### Support ###

If you have a question about **Tapir**, please contact us at 
[support@sip3.io](mailto:support@sip3.io "send mail to tapir team"). We are always ready to help you.

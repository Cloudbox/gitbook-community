[Varken](https://github.com/Boerderij/Varken) (by DirtyCajunRice/samwiseg0) is a standalone command-line utility to aggregate data from the Plex ecosystem into InfluxDB. Examples use Grafana for a frontend.


1. Run the cloudbox varken feature to install varken/influxdb/telegraf/grafana:
   ```bash
   cd ~/cloudbox
   sudo ansible-playbook cloudbox.yml --tags varken
   ```
2. Add your Maxmind API key to varken.ini:
   ```bash
   nano /opt/varken/varken.ini
   ```
3. Restart Varken:
   ```bash
   docker restart varken
   ```
4. Visit grafana https://grafana.domain.com - default login is admin and your default CB password. 

5. Add data source InfluxDB named InfluxDB:

   **HTTP**: URL = http://influxdb:8086

   **InfluxDB Details**: Database = varken

   Save & Test

6. Add data source InfluxDB named Telegraf:

   **HTTP**: URL = http://influxdb:8086

   **InfluxDB Details**: Database = telegraf

   Save & Test

7. Grafana Example from Organizrr Discord  (imported via Dashboards > Manage > Import) :

   from: GilbN -- Plex dashboard for Grafana
   @Grafana-Group for anyone using Varken (https://github.com/Boerderij/Varken) Thought I'd share the dashboard I made 
   (with the help of Rox and Tron): https://grafana.com/dashboards/9558
   You will need to add the piechart and worldmap plugins for the dashboard to work. Use the variables to set the 
   different 
   data sources.

   To Install PieChart/WorldMap:
   `cd /opt/grafana/plugins && git clone https://github.com/grafana/piechart-panel.git && git clone 
    https://github.com/grafana/worldmap-panel.git && docker restart grafana`

   ![](https://grafana.com/api/dashboards/9558/images/5941/image)
8. Grafana Examples from Varken Discord:

   **Varken Official Supported Dashboards:** https://grafana.com/dashboards?search=varken%20%5Bofficial%5D
   
   **Online Users Table Example (Tautulli):** https://gist.github.com/samwiseg0/91223c1e089d78a3ae6294c23d81e977

   **World Map w/ geoIP**

   ![](https://i.imgur.com/2Qh73bR.png)
   ![](https://i.imgur.com/0ks1ZxR.png)

   **Device Type Pie Chart:** https://gist.github.com/samwiseg0/fab103fdf4b176a11517e478ce7c216f

   **Basic Panel Structure**

   ![](https://i.imgur.com/iM7pq5e.png)

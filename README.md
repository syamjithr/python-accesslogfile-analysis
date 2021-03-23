# python-accesslogfile-analysis
# Log file Analysis using Python
You can use simple python codes to organize and analyze your log files like access_log. The bleow code will return a chart with ip and number of hits. For ploting the chart we used  matplotlib.pyplot module.
```
log = open('access.log')

date_hits = {}

for logLine in log:

  line = logLine.split()

  ip = line[0]

  date = line[3].lstrip('[')

  date = date[0:11]
   
  if date in date_hits:
    if ip in date_hits[date]:
      date_hits[date][ip] = date_hits[date][ip] + 1
    else:
      date_hits[date].update({ip:1})
  else:
    date_hits.update({date:{ip:1}})
```
```
import matplotlib.pyplot as plt
ip_List = []
MaxHit = []
for item in date_hits:
  
  keys_list = list(date_hits[item].keys())
  values_list = list(date_hits[item].values())
  Max_hit = max(values_list)
  position = values_list.index(Max_hit)
  ip = keys_list[position]
  ip_List.append(ip)
  MaxHit.append(Max_hit)
plt.figure(figsize=(10, 10))
plt.title('HitPerDay')
plt.ylabel('From IP')
plt.xlabel('Number of Hits')
plt.barh(ip_List,MaxHit)
plt.show()
```
#### output
![hit_per_ip](https://user-images.githubusercontent.com/75690151/112109323-6b569d00-8bd7-11eb-9c4f-c55c61271469.png)

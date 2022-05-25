# Simple python Grafana Loki API client

## Usage
```
from loki import Loki

now = datetime.now(tz=pytz.timezone('Europe/Moscow'))
some_time_ago = now - timedelta(minutes=5)
loki = Loki(limit=1000)

labels = loki.get_label_values('host', some_time_ago, now)

labels_values = loki.get_label_values('host', some_time_ago, now)

data = loki.query('{host="localhost", job="nginx"}', start=some_time_ago, end=now)

for s in loki.iterate_streams('{job="%s"}' % good_job_name, now - timedelta(minutes=30), now, lines_limit=lines_limit):
    print(s.stream, len(s.values))

```


Tested whith python 3.9

## TODO:
- Use requests.Session() to persist connection
- Intercept requests connection exceptions <https://docs.python-requests.org/en/latest/user/advanced/>

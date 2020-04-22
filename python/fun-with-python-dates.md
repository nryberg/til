# Fun with Python Dates

Python gives you some flexible tools for managing dates.  My goal was to get URL ready epoch timestamps for yesterday and today.

```python
# Get the epoch for the delta
epoch = datetime.date(1970,1,1)

# Incremental value for math
one_day = datetime.timedelta(days=1)

today = datetime.date.today()

# Everything else is gravy
yesterday = today - one_day

# Total Seconds in string format includes a .0.  That needs to be dropped
end = str((today - epoch).total_seconds()).split('.')[0]
begin = str((yesterday - epoch).total_seconds()).split('.')[0]
```

This results in:

* Begin = '1587427200'
* End = '1587513600'
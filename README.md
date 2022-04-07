# week-of-mount-with-python

contoh olah data csv dengan py
```PY
import pytz, datetime, pendulum, json, csv
from datetime import datetime, timedelta
import numpy as np
import pandas as pd
import calendar
import numpy as np

calendar.setfirstweekday(6)

dataset = pd.read_csv("dataset.csv", encoding="ISO-8859-1")
dataset.head()

aod = dataset["ApointmentData"]

data = {}

datawom = []

for row in aod:
    xplit = row.split("T")[0]
    if row in aod:
        data[row] += xplit
    else:
        data[row] = xplit

    # def getTime():
    #    tz = pytz.timezone("Asia/Jakarta")
    #    timeNow = datetime.now(tz=tz)
    #    localtimes = datetime.strftime(timeNow, "%Y-%m-%d")
    #    return localtimes


    def prettyPrint(djson, ind=4):
        print(json.dumps(djson, indent=ind, sort_keys=True))


    def wom_pendlum(dateData):
        dt = pendulum.parse(str(dateData))
        wom = dt.week_of_month
        return wom


    def get_week_of_month(year, month, day):
        x = np.array(calendar.monthcalendar(year, month))
        week_of_month = np.where(x == day)[0][0] + 1
        return week_of_month


    parameter = 2  # // untuk nentuin itung pake wom_pendlum /  get_week_of_month

    # using // get_week_of_month //
    if parameter == 1:
        cnt = 0
        for x in data:
            if cnt != 3:  # << apus aja kalo mau print semua data
                xdata = data[x]
                datesplit = xdata.split("-")
                years = datesplit[0]
                mount = datesplit[1]
                days = datesplit[2]
                xres = {x: str(get_week_of_month(int(years), int(mount), int(days)))}
                datawom.append(xres)
                cnt += 1

    # using // wom_pendlum //
    if parameter == 2:
        cnt = 0
        for x in data:
            if cnt != 3:  # << apus aja kalo mau print semua data
                xdata = data[x]
                xres = {x: wom_pendlum(xdata)}
                datawom.append(xres)
                cnt += 1

    prettyPrint(datawom)
```

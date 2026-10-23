# 💫 About Me:
🎓 B.Tech CSE (AI & ML) student at Amity University Jharkhand.<br>💻 Exploring AI, Machine Learning, and software development through hands-on projects.<br>🚀 Always learning, building, and turning ideas into real-world solutions.<br>


## 🌐 Socials:
[![Instagram](https://img.shields.io/badge/Instagram-%23E4405F.svg?logo=Instagram&logoColor=white)](https://instagram.com/https://www.instagram.com/shreshth_1006?utm_source=qr&mdxt=MXY3NnJncHF5OXZhbw==) [![LinkedIn](https://img.shields.io/badge/LinkedIn-%230077B5.svg?logo=linkedin&logoColor=white)](https://linkedin.com/in/https://www.linkedin.com/in/shreshth-07131a383?utm_source=share_via&utm_content=profile&utm_medium=member_android) [![X](https://img.shields.io/badge/X-black.svg?logo=X&logoColor=white)](https://x.com/https://x.com/Shreshth1006) [![Mastodon](https://img.shields.io/badge/-MASTODON-%232B90D9?logo=mastodon&logoColor=white)](https://mastodon.social/@SHRESHTH) [![email](https://img.shields.io/badge/Email-D14836?logo=gmail&logoColor=white)](mailto:s.shreshth1006@gmail.com) 

# 💻 Tech Stack:
![HTML5](https://img.shields.io/badge/html5-%23E34F26.svg?style=for-the-badge&logo=html5&logoColor=white) ![CSS3](https://img.shields.io/badge/css3-%231572B6.svg?style=for-the-badge&logo=css3&logoColor=white) ![C](https://img.shields.io/badge/c-%2300599C.svg?style=for-the-badge&logo=c&logoColor=white) ![C#](https://img.shields.io/badge/c%23-%23239120.svg?style=for-the-badge&logo=csharp&logoColor=white) ![C++](https://img.shields.io/badge/c++-%2300599C.svg?style=for-the-badge&logo=c%2B%2B&logoColor=white) ![Python](https://img.shields.io/badge/python-3670A0?style=for-the-badge&logo=python&logoColor=ffdd54) ![JavaScript](https://img.shields.io/badge/javascript-%23323330.svg?style=for-the-badge&logo=javascript&logoColor=%23F7DF1E) ![Firebase](https://img.shields.io/badge/firebase-%23039BE5.svg?style=for-the-badge&logo=firebase) ![Vercel](https://img.shields.io/badge/vercel-%23000000.svg?style=for-the-badge&logo=vercel&logoColor=white) ![FastAPI](https://img.shields.io/badge/FastAPI-005571?style=for-the-badge&logo=fastapi) ![Express.js](https://img.shields.io/badge/express.js-%23404d59.svg?style=for-the-badge&logo=express&logoColor=%2361DAFB) ![Firebase](https://img.shields.io/badge/firebase-a08021?style=for-the-badge&logo=firebase&logoColor=ffcd34) ![SQLite](https://img.shields.io/badge/sqlite-%2307405e.svg?style=for-the-badge&logo=sqlite&logoColor=white) ![Supabase](https://img.shields.io/badge/Supabase-3ECF8E?style=for-the-badge&logo=supabase&logoColor=white) ![MySQL](https://img.shields.io/badge/mysql-4479A1.svg?style=for-the-badge&logo=mysql&logoColor=white) ![Canva](https://img.shields.io/badge/Canva-%2300C4CC.svg?style=for-the-badge&logo=Canva&logoColor=white) ![Matplotlib](https://img.shields.io/badge/Matplotlib-%23ffffff.svg?style=for-the-badge&logo=Matplotlib&logoColor=black) ![Pandas](https://img.shields.io/badge/pandas-%23150458.svg?style=for-the-badge&logo=pandas&logoColor=white) ![Plotly](https://img.shields.io/badge/Plotly-%233F4F75.svg?style=for-the-badge&logo=plotly&logoColor=white) ![scikit-learn](https://img.shields.io/badge/scikit--learn-%23F7931E.svg?style=for-the-badge&logo=scikit-learn&logoColor=white) ![NumPy](https://img.shields.io/badge/numpy-%23013243.svg?style=for-the-badge&logo=numpy&logoColor=white) ![Epic Games](https://img.shields.io/badge/epicgames-%23313131.svg?style=for-the-badge&logo=epicgames&logoColor=white) ![GitHub](https://img.shields.io/badge/github-%23121011.svg?style=for-the-badge&logo=github&logoColor=white) ![Git](https://img.shields.io/badge/git-%23F05033.svg?style=for-the-badge&logo=git&logoColor=white)
# 📊 GitHub Stats:
![](https://github-readme-stats.shion.dev/api?username=Shreshth-1006&theme=dark&hide_border=false&include_all_commits=false&count_private=false)<br/>
![](https://streak-stats.demolab.com/?user=Shreshth-1006&theme=dark&hide_border=false)<br/>
![](https://github-readme-stats.shion.dev/api/top-langs/?username=Shreshth-1006&theme=dark&hide_border=false&include_all_commits=false&count_private=false&layout=compact)

<!-- Proudly created with GPRM ( https://gprm.itsvg.in ) -->
"""
Code City  (v2)
---------------
Turns your last year of GitHub contributions into a night-time cyberpunk skyline.

  - one building = one week   (taller = busier week)
  - one window   = one day    (lit window = you coded that day, Sunday at the bottom)
  - oldest week on the left, this week on the right (with a searchlight on top)
  - your best week gets a neon billboard
  - month labels on the pavement, street lamps, cars, flying drones, a blimp,
    drifting clouds, a moon, a shooting star and a flickering neon sign

No dependencies. Pure Python 3.

Test locally (fake data, no token):  python generate_skyline.py --demo
Real run:  GH_USER=Shreshth-1006 GITHUB_TOKEN=xxxx python generate_skyline.py
"""

import json
import os
import random
import sys
import urllib.request
from datetime import date, datetime, timedelta

USER = os.environ.get("GH_USER", "Shreshth-1006")
TOKEN = os.environ.get("GITHUB_TOKEN", "")
OUT = os.environ.get("OUT", "assets/skyline.svg")

W, H = 900, 372
GROUND = 300       # y of the pavement
WIN_PITCH = 9      # vertical distance between windows
MAX_EXTRA = 100    # extra height for the busiest week
MONTHS = ["Jan", "Feb", "Mar", "Apr", "May", "Jun", "Jul", "Aug", "Sep", "Oct", "Nov", "Dec"]

# lit-window colour by level (1..4)
LIT = {1: "#ffe9a8", 2: "#ffd166", 3: "#ff9f43", 4: "#5ef2ff"}


def fetch_days():
    query = """
    query($login: String!) {
      user(login: $login) {
        contributionsCollection {
          contributionCalendar {
            weeks { contributionDays { date contributionCount } }
          }
        }
      }
    }"""
    body = json.dumps({"query": query, "variables": {"login": USER}}).encode()
    req = urllib.request.Request(
        "https://api.github.com/graphql",
        data=body,
        headers={"Authorization": f"bearer {TOKEN}", "Content-Type": "application/json"},
    )
    with urllib.request.urlopen(req, timeout=30) as r:
        data = json.load(r)
    weeks = data["data"]["user"]["contributionsCollection"]["contributionCalendar"]["weeks"]
    return [(d["date"], d["contributionCount"]) for w in weeks for d in w["contributionDays"]]


def fake_days():
    rnd = random.Random(11)
    start = date.today() - timedelta(days=364)
    days = []
    for i in range(365):
        day = start + timedelta(days=i)
        n = 0 if rnd.random() < 0.32 else int(rnd.expovariate(0.4))
        days.append((day.isoformat(), min(n, 22)))
    return days


def group_weeks(days):
    """Return [(week_start_date, [7 counts, Sunday first]), ...]."""
    weeks, current, last_key = [], [0] * 7, None
    for ds, c in days:
        d = datetime.strptime(ds, "%Y-%m-%d").date()
        dow = (d.weekday() + 1) % 7  # Sunday = 0
        key = d - timedelta(days=dow)
        if last_key is not None and key != last_key:
            weeks.append((last_key, current))
            current = [0] * 7
        current[dow] = c
        last_key = key
    weeks.append((last_key, current))
    return weeks


def level(count, peak):
    if count == 0:
        return 0
    r = count / max(peak, 1)
    return 4 if r > 0.75 else 3 if r > 0.45 else 2 if r > 0.2 else 1


CSS = """
    text{font-family:'Courier New',monospace}
    .tw{animation:tw 3s ease-in-out infinite}
    @keyframes tw{0%,100%{opacity:.25}50%{opacity:1}}
    .fl{animation:fl 4s ease-in-out infinite}
    @keyframes fl{0%,100%{opacity:1}45%{opacity:.8}50%{opacity:.45}55%{opacity:.9}}
    .bk{animation:bk 1.6s steps(1) infinite}
    @keyframes bk{0%{opacity:1}50%{opacity:.1}}
    .neon{animation:neon 6s linear infinite}
    @keyframes neon{0%,18%,22%,62%,64%,100%{opacity:1}20%,63%{opacity:.35}}
    .sign{animation:sign 3.2s linear infinite}
    @keyframes sign{0%,40%,44%,100%{opacity:1}42%{opacity:.3}}
    .car1{animation:r 15s linear infinite}
    .car2{animation:l 22s linear infinite}
    .car3{animation:r 28s linear infinite;animation-delay:-9s}
    @keyframes r{from{transform:translateX(-80px)}to{transform:translateX(990px)}}
    @keyframes l{from{transform:translateX(990px)}to{transform:translateX(-80px)}}
    .drone1{animation:r 20s linear infinite;animation-delay:-4s}
    .drone2{animation:l 31s linear infinite;animation-delay:-14s}
    .blimp{animation:blimp 60s linear infinite;animation-delay:-18s}
    @keyframes blimp{from{transform:translateX(-140px)}to{transform:translateX(1050px)}}
    .cloud1{animation:cl 90s linear infinite}
    .cloud2{animation:cl 130s linear infinite;animation-delay:-60s}
    @keyframes cl{from{transform:translateX(-200px)}to{transform:translateX(1100px)}}
    .moon{animation:moon 8s ease-in-out infinite alternate}
    @keyframes moon{from{transform:translateY(0)}to{transform:translateY(4px)}}
    .beam{animation:beam 7s ease-in-out infinite alternate}
    @keyframes beam{from{transform:rotate(-24deg)}to{transform:rotate(24deg)}}
    .shoot{animation:shoot 11s linear infinite;opacity:0}
    @keyframes shoot{0%{transform:translate(0,0);opacity:0}2%{opacity:1}11%{transform:translate(340px,150px);opacity:0}100%{transform:translate(340px,150px);opacity:0}}
    .lamp{animation:lamp 5s ease-in-out infinite}
    @keyframes lamp{0%,100%{opacity:.85}50%{opacity:1}}
"""


def build(days):
    rnd = random.Random(5)
    weeks = group_weeks(days)
    n = len(weeks)
    peak_day = max(c for _, c in days) or 1
    totals = [sum(w) for _, w in weeks]
    max_week = max(totals) or 1
    total = sum(totals)
    active = sum(1 for _, c in days if c)
    longest = run = 0
    for _, c in days:
        run = run + 1 if c else 0
        longest = max(longest, run)
    busiest = totals.index(max(totals))

    margin = 22
    slot = (W - 2 * margin) / n
    bw = slot - 2.4

    def b_height(i):
        return 7 * WIN_PITCH + 16 + MAX_EXTRA * (totals[i] / max_week)

    o = []
    a = o.append
    a(f'<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 {W} {H}" width="100%" role="img" '
      f'aria-label="{USER} code city: {total} contributions">')
    a(f"""<defs>
  <linearGradient id="sky" x1="0" y1="0" x2="0" y2="1">
    <stop offset="0" stop-color="#05050f"/><stop offset=".45" stop-color="#171240"/>
    <stop offset=".8" stop-color="#43205e"/><stop offset="1" stop-color="#7a2f6b"/>
  </linearGradient>
  <linearGradient id="fog" x1="0" y1="0" x2="0" y2="1">
    <stop offset="0" stop-color="#7a2f6b" stop-opacity="0"/><stop offset="1" stop-color="#b8479a" stop-opacity=".38"/>
  </linearGradient>
  <linearGradient id="beamg" x1="0" y1="1" x2="0" y2="0">
    <stop offset="0" stop-color="#9ffcff" stop-opacity=".55"/><stop offset="1" stop-color="#9ffcff" stop-opacity="0"/>
  </linearGradient>
  <linearGradient id="lampg" x1="0" y1="0" x2="0" y2="1">
    <stop offset="0" stop-color="#ffd9a0" stop-opacity=".5"/><stop offset="1" stop-color="#ffd9a0" stop-opacity="0"/>
  </linearGradient>
  <filter id="glow" x="-60%" y="-60%" width="220%" height="220%"><feGaussianBlur stdDeviation="2"/></filter>
  <filter id="glow2" x="-30%" y="-80%" width="160%" height="260%"><feGaussianBlur stdDeviation="3.5"/></filter>
  <filter id="soft" x="-30%" y="-30%" width="160%" height="160%"><feGaussianBlur stdDeviation="6"/></filter>
  <style>{CSS}</style>
</defs>""")
    a(f'<rect width="{W}" height="{H}" rx="14" fill="url(#sky)"/>')

    # stars
    for _ in range(110):
        x, y = rnd.uniform(0, W), rnd.uniform(0, 170)
        d, dl = rnd.uniform(2, 6), rnd.uniform(0, 6)
        a(f'<circle class="tw" cx="{x:.0f}" cy="{y:.0f}" r="{rnd.choice([.6,.8,1.1])}" fill="#fff" '
          f'style="animation-duration:{d:.1f}s;animation-delay:{dl:.1f}s"/>')

    # shooting star
    a('<g class="shoot"><line x1="60" y1="24" x2="106" y2="46" stroke="#fff" stroke-width="1.6" stroke-linecap="round" opacity=".9"/>'
      '<circle cx="106" cy="46" r="2" fill="#fff"/></g>')

    # moon + clouds
    a('<g class="moon"><circle cx="810" cy="66" r="34" fill="#ffe9a8" opacity=".28" filter="url(#glow2)"/>'
      '<circle cx="810" cy="66" r="20" fill="#fff4cf"/>'
      '<circle cx="803" cy="61" r="3.6" fill="#e8d9a0"/><circle cx="817" cy="72" r="2.6" fill="#e8d9a0"/>'
      '<circle cx="815" cy="58" r="1.8" fill="#e8d9a0"/></g>')
    a('<g class="cloud1" opacity=".16" fill="#cdbdff"><ellipse cx="0" cy="92" rx="70" ry="9"/><ellipse cx="30" cy="86" rx="40" ry="8"/></g>')
    a('<g class="cloud2" opacity=".12" fill="#cdbdff"><ellipse cx="0" cy="138" rx="90" ry="10"/><ellipse cx="-34" cy="132" rx="46" ry="8"/></g>')

    # blimp
    a('<g class="blimp"><g transform="translate(0,110)">'
      '<ellipse cx="0" cy="0" rx="24" ry="7.5" fill="#2b2f55"/><ellipse cx="-3" cy="-2" rx="16" ry="2" fill="#5a62a0" opacity=".6"/>'
      '<rect x="-4" y="6" width="9" height="3.4" rx="1" fill="#2b2f55"/>'
      '<circle class="bk" cx="24" cy="0" r="1.7" fill="#ff4d4d"/><circle class="bk" cx="-24" cy="0" r="1.7" fill="#4dff88"/>'
      '</g></g>')

    # flying drones with light trails
    a('<g class="drone1"><g transform="translate(0,150)"><line x1="-26" y1="0" x2="0" y2="0" stroke="#5ef2ff" stroke-opacity=".5" stroke-width="1.4"/>'
      '<rect x="0" y="-2" width="7" height="4" rx="2" fill="#5ef2ff"/><circle cx="7" cy="0" r="5" fill="#5ef2ff" opacity=".4" filter="url(#glow)"/></g></g>')
    a('<g class="drone2"><g transform="translate(0,176)"><line x1="26" y1="0" x2="0" y2="0" stroke="#ff7ad9" stroke-opacity=".5" stroke-width="1.4"/>'
      '<rect x="-7" y="-2" width="7" height="4" rx="2" fill="#ff7ad9"/><circle cx="-7" cy="0" r="5" fill="#ff7ad9" opacity=".4" filter="url(#glow)"/></g></g>')

    # two far skyline layers for depth
    for layer, (col, hmin, hmax, wmin, wmax, dots) in enumerate([
            ("#241846", 70, 150, 16, 34, 0.5), ("#16102f", 40, 110, 18, 40, 0.25)]):
        x = -10
        a(f'<g fill="{col}">')
        lights = []
        while x < W:
            w = rnd.uniform(wmin, wmax)
            h = rnd.uniform(hmin, hmax)
            a(f'<rect x="{x:.0f}" y="{GROUND-h:.0f}" width="{w:.0f}" height="{h:.0f}"/>')
            for _ in range(int(w * h / 420)):
                if rnd.random() < dots:
                    lights.append((x + rnd.uniform(2, w - 3), GROUND - rnd.uniform(6, h - 4)))
            x += w + rnd.uniform(0, 5)
        a("</g>")
        a('<g fill="#ffd9a0" opacity=".45">' +
          "".join(f'<rect x="{lx:.0f}" y="{ly:.0f}" width="2" height="2"/>' for lx, ly in lights) + "</g>")

    # the real buildings
    shades = ["#1b1f3d", "#1f2347", "#171a35", "#22264d"]
    for i, (wstart, week) in enumerate(weeks):
        bx = margin + i * slot
        bh = b_height(i)
        by = GROUND - bh
        body = rnd.choice(shades)
        a(f'<g><title>Week of {wstart}: {totals[i]} contributions</title>')
        a(f'<rect x="{bx:.1f}" y="{by:.1f}" width="{bw:.1f}" height="{bh:.1f}" fill="{body}"/>')
        a(f'<rect x="{bx+bw*0.74:.1f}" y="{by:.1f}" width="{bw*0.26:.1f}" height="{bh:.1f}" fill="#000" opacity=".28"/>')
        a(f'<rect x="{bx:.1f}" y="{by:.1f}" width="{bw:.1f}" height="1.4" fill="#3a4180"/>')

        extra = bh - (7 * WIN_PITCH + 16)
        style = rnd.random()
        cx = bx + bw / 2
        if extra > 70:
            a(f'<rect x="{bx+bw*0.2:.1f}" y="{by-9:.1f}" width="{bw*0.6:.1f}" height="9" fill="{body}"/>')
            a(f'<line x1="{cx:.1f}" y1="{by-9:.1f}" x2="{cx:.1f}" y2="{by-25:.1f}" stroke="#4a5290" stroke-width="1"/>')
            a(f'<circle class="bk" cx="{cx:.1f}" cy="{by-25:.1f}" r="1.6" fill="#ff4d4d" style="animation-delay:{rnd.uniform(0,1.6):.1f}s"/>')
        elif extra > 30 and style < 0.45:
            a(f'<path d="M{bx:.1f} {by:.1f} L{bx+bw:.1f} {by-7:.1f} L{bx+bw:.1f} {by:.1f}Z" fill="#2c3263"/>')
        elif extra > 30 and style < 0.75:
            a(f'<rect x="{bx+2:.1f}" y="{by-6:.1f}" width="{bw*0.45:.1f}" height="6" fill="#272c58"/>'
              f'<rect x="{bx+3:.1f}" y="{by-9:.1f}" width="2" height="3" fill="#3a4180"/>')
        elif rnd.random() < 0.35:
            a(f'<ellipse cx="{cx:.1f}" cy="{by:.1f}" rx="{bw*0.4:.1f}" ry="3.5" fill="#2c3263"/>')

        # windows: Sunday at the bottom, Saturday at the top
        wx = bx + bw * 0.2
        ww = bw * 0.5
        for d in range(7):
            wy = GROUND - 14 - d * WIN_PITCH
            c = week[d]
            lv = level(c, peak_day)
            if lv == 0:
                a(f'<rect x="{wx:.1f}" y="{wy:.1f}" width="{ww:.1f}" height="5" fill="#0a0c1c" opacity=".9"/>')
                continue
            col = LIT[lv]
            if lv >= 3:
                a(f'<rect x="{wx-1.2:.1f}" y="{wy-1.2:.1f}" width="{ww+2.4:.1f}" height="7.4" fill="{col}" opacity=".6" filter="url(#glow)"/>')
            a(f'<rect class="fl" x="{wx:.1f}" y="{wy:.1f}" width="{ww:.1f}" height="5" fill="{col}" '
              f'style="animation-duration:{rnd.uniform(3,7):.1f}s;animation-delay:{rnd.uniform(0,5):.1f}s"/>')
            if lv >= 3:  # reflection on the wet road
                a(f'<rect x="{wx:.1f}" y="{GROUND+16+d*3:.1f}" width="{ww:.1f}" height="1.6" fill="{col}" opacity=".18"/>')
        a("</g>")

    # fog hugging the street
    a(f'<rect x="0" y="{GROUND-80}" width="{W}" height="80" fill="url(#fog)"/>')

    # neon billboard on the busiest week
    bi = busiest
    bcx = margin + bi * slot + bw / 2
    btop = GROUND - b_height(bi) - 34
    bwid = 92
    bx0 = min(max(bcx - bwid / 2, 6), W - bwid - 6)
    a(f'<g class="sign"><line x1="{bcx-8:.1f}" y1="{btop+22:.1f}" x2="{bcx-8:.1f}" y2="{btop+34:.1f}" stroke="#4a5290"/>'
      f'<line x1="{bcx+8:.1f}" y1="{btop+22:.1f}" x2="{bcx+8:.1f}" y2="{btop+34:.1f}" stroke="#4a5290"/>'
      f'<rect x="{bx0:.1f}" y="{btop:.1f}" width="{bwid}" height="22" rx="3" fill="#ff2e97" opacity=".35" filter="url(#glow)"/>'
      f'<rect x="{bx0:.1f}" y="{btop:.1f}" width="{bwid}" height="22" rx="3" fill="#1a0a2e" stroke="#ff2e97" stroke-width="1.4"/>'
      f'<text x="{bx0+bwid/2:.1f}" y="{btop+9:.1f}" fill="#ff9ad5" font-size="7" text-anchor="middle" letter-spacing="1.5">BEST WEEK</text>'
      f'<text x="{bx0+bwid/2:.1f}" y="{btop+19:.1f}" fill="#fff" font-size="10" font-weight="bold" text-anchor="middle">{totals[bi]} commits</text></g>')

    # searchlight on today's building
    lx = margin + (n - 1) * slot + bw / 2
    ltop = GROUND - b_height(n - 1)
    a(f'<g transform="translate({lx:.1f},{ltop:.1f})"><g class="beam" style="transform-origin:0 0">'
      f'<polygon points="0,0 -26,-190 26,-190" fill="url(#beamg)"/></g>'
      f'<circle r="3" fill="#9ffcff"/><circle r="7" fill="#9ffcff" opacity=".4" filter="url(#glow)"/></g>')
    a(f'<g class="bk"><text x="{lx-10:.0f}" y="{ltop-14:.0f}" fill="#00f5a0" font-size="10" font-weight="bold" text-anchor="end">today</text></g>')

    # pavement + month labels, road, lane marks
    a(f'<rect x="0" y="{GROUND}" width="{W}" height="14" fill="#14122e"/>')
    a(f'<rect x="0" y="{GROUND}" width="{W}" height="2" fill="#3a4180"/>')
    prev = None
    for i, (wstart, _) in enumerate(weeks):
        if wstart.month != prev:
            if i > 0 or n < 6:
                a(f'<text x="{margin+i*slot:.0f}" y="{GROUND+10}" fill="#7f86c0" font-size="8">{MONTHS[wstart.month-1]}</text>')
            prev = wstart.month
    a(f'<rect x="0" y="{GROUND+14}" width="{W}" height="{H-GROUND-14}" fill="#0a0a18"/>')
    for rx in range(0, W, 46):
        a(f'<rect x="{rx}" y="{GROUND+34}" width="22" height="2" fill="#3a3f70"/>')

    # street lamps
    for lx2 in range(60, W, 150):
        a(f'<g class="lamp"><polygon points="{lx2-16},{GROUND+14} {lx2+16},{GROUND+14} {lx2+5},{GROUND-30} {lx2-5},{GROUND-30}" fill="url(#lampg)" opacity=".5"/>'
          f'<line x1="{lx2}" y1="{GROUND+12}" x2="{lx2}" y2="{GROUND-30}" stroke="#2c3263" stroke-width="2"/>'
          f'<circle cx="{lx2}" cy="{GROUND-31}" r="2.6" fill="#ffd9a0"/><circle cx="{lx2}" cy="{GROUND-31}" r="7" fill="#ffd9a0" opacity=".45" filter="url(#glow)"/></g>')

    # cars
    a(f'<g class="car1"><g transform="translate(0,{GROUND+20})"><rect width="26" height="8" rx="3" fill="#ff4d6d"/>'
      '<rect x="6" y="-4" width="13" height="5" rx="2" fill="#c9304d"/>'
      '<polygon points="26,1 56,-3 56,11 26,7" fill="#fff6c9" opacity=".18"/>'
      '<circle cx="26" cy="4" r="6" fill="#fff6c9" opacity=".4" filter="url(#glow)"/><circle cx="25" cy="4" r="1.6" fill="#fff6c9"/>'
      '<rect x="0" y="2" width="2" height="3" fill="#ff1a1a"/></g></g>')
    a(f'<g class="car3"><g transform="translate(0,{GROUND+20})"><rect width="24" height="8" rx="3" fill="#a56bff"/>'
      '<rect x="5" y="-4" width="12" height="5" rx="2" fill="#7a3fd6"/>'
      '<circle cx="24" cy="4" r="6" fill="#fff6c9" opacity=".4" filter="url(#glow)"/><circle cx="23" cy="4" r="1.6" fill="#fff6c9"/>'
      '<rect x="0" y="2" width="2" height="3" fill="#ff1a1a"/></g></g>')
    a(f'<g class="car2"><g transform="translate(0,{GROUND+38})"><rect width="26" height="8" rx="3" fill="#4d9bff"/>'
      '<rect x="7" y="-4" width="13" height="5" rx="2" fill="#2b6fd1"/>'
      '<polygon points="0,1 -30,-3 -30,11 0,7" fill="#fff6c9" opacity=".18"/>'
      '<circle cx="0" cy="4" r="6" fill="#fff6c9" opacity=".4" filter="url(#glow)"/><circle cx="1" cy="4" r="1.6" fill="#fff6c9"/>'
      '<rect x="24" y="2" width="2" height="3" fill="#ff1a1a"/></g></g>')

    # neon title + stats
    a('<g class="neon"><text x="24" y="38" fill="#00f5a0" font-size="18" font-weight="bold" letter-spacing="5" opacity=".6" filter="url(#glow2)">CODE CITY</text>'
      '<text x="24" y="38" fill="#d9fff0" font-size="18" font-weight="bold" letter-spacing="5">CODE CITY</text></g>')
    a(f'<text x="24" y="56" fill="#9a9fd4" font-size="11">@{USER}</text>')
    a(f'<text x="24" y="{H-8}" fill="#9a9fd4" font-size="10">'
      f'{total} contributions  |  {active} active days  |  longest streak {longest}  |  busiest week #{busiest+1}</text>')
    a(f'<text x="{W-24}" y="{H-8}" fill="#6b72a8" font-size="10" text-anchor="end">building = week  ·  window = day  ·  lit = coded</text>')
    a("</svg>")
    return "\n".join(o)


def main():
    if "--demo" in sys.argv or not TOKEN:
        print("No token found or --demo used: building with fake data.")
        days = fake_days()
    else:
        days = fetch_days()
    svg = build(days)
    os.makedirs(os.path.dirname(OUT) or ".", exist_ok=True)
    with open(OUT, "w", encoding="utf-8") as f:
        f.write(svg)
    print(f"Wrote {OUT} ({len(svg)//1024} KB)")


if __name__ == "__main__":
    main()

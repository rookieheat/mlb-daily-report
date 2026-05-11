import requests
from datetime import datetime

def get_today_games():
    today = datetime.utcnow().strftime("%Y-%m-%d")
    url = f"https://statsapi.mlb.com/api/v1/schedule?date={today}&sportId=1"
    r = requests.get(url)
    r.raise_for_status()
    data = r.json()

    lines = [f"MLB Games for {today}"]
    if not data.get("dates"):
        lines.append("No games today.")
        return "\n".join(lines)

    games = data["dates"][0]["games"]
    for g in games:
        away = g["teams"]["away"]["team"]["name"]
        home = g["teams"]["home"]["team"]["name"]
        status = g["status"]["detailedState"]
        lines.append(f"{away} @ {home} - {status}")
    return "\n".join(lines)

def main():
    report = get_today_games()
    with open("daily_report.txt", "w", encoding="utf-8") as f:
        f.write(report + "\n\n(You can later add card data here.)")

if __name__ == "__main__":
    main()

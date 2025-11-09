from datetime import date, datetime

def calculate_age(birth_date):
    today = date.today()
    years = today.year - birth_date.year
    months = today.month - birth_date.month
    days = today.day - birth_date.day

    # Adjust for negative months/days
    if days < 0:
        months -= 1
        prev_month = (today.month - 1) or 12
        prev_year = today.year if today.month != 1 else today.year - 1
        days_in_prev_month = (date(prev_year, prev_month % 12 + 1, 1) - date(prev_year, prev_month, 1)).days
        days += days_in_prev_month

    if months < 0:
        years -= 1
        months += 12

    return years, months, days

def next_birthday(birth_date):
    today = date.today()
    next_bday = date(today.year, birth_date.month, birth_date.day)

    if next_bday < today:
        next_bday = date(today.year + 1, birth_date.month, birth_date.day)

    days_until = (next_bday - today).days
    return next_bday, days_until

def main():
    print("🎂 Welcome to the Smart Age Calculator 🎂")
    print("---------------------------------------")

    # Take input
    bday_str = input("Enter your birth date (DD-MM-YYYY): ")

    try:
        birth_date = datetime.strptime(bday_str, "%d-%m-%Y").date()
    except ValueError:
        print("⚠️ Invalid date format! Please use DD-MM-YYYY.")
        return

    years, months, days = calculate_age(birth_date)
    print(f"\n📅 You are {years} years, {months} months, and {days} days old.")

    # Next birthday info
    next_bday, days_left = next_birthday(birth_date)
    print(f"🎈 Your next birthday is on {next_bday.strftime('%A, %d %B %Y')}.")
    print(f"⏳ Days until next birthday: {days_left} days!")

    # Fun message
    if days_left == 0:
        print("🎉 Happy Birthday! 🥳")
    elif days_left <= 7:
        print("🎁 Your birthday is coming soon — get ready to celebrate!")
    else:
        print("😊 Have a great year ahead!")

if __name__ == "__main__":
    main()


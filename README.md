# pass_checker
Password Strength Checker tool built to evaluate password strength and compliance with organizational standards.

Sample Project #3

The goal was to create a script that I could feed passwords for testing against organization standards; 

    Minimum of 12 characters, 
    Lower case and upper case letters, 
    Numbers, 
    Special characters,
    Does not appear on a password list

Steps:

1. I ensured that Python 3 was installed (it was) and verified the version (python 3.13)

2. I created a .py file by opening Notepad++ and creating a file called pass_checker.py and saved the file.
3. I verified that the file was created and was a py file
4. I created a text file called "weaklist.txt" containing passwords, on per line, that do not meet organization standards.
5. I opened the pass_checker.py file in Notepad++ and wrote the following:

		import re
    	from colorama import Fore, Style, init

    	# Initialize colorama for Windows compatibility
    	init(autoreset=True)

    	def check_password_strength(password):
      	checks_passed = []
      	checks_failed = []

    	# Length check (>= 12)
    	if len(password) >= 12:
        	checks_passed.append("Length (12+ characters)")
    	else:
        	checks_failed.append("Length (12+ characters)")

    	# Uppercase letter check
    	if re.search(r"[A-Z]", password):
        	checks_passed.append("Uppercase letter")
    	else:
        	checks_failed.append("Uppercase letter")

    	# Lowercase letter check
    	if re.search(r"[a-z]", password):
        	checks_passed.append("Lowercase letter")
    	else:
        	checks_failed.append("Lowercase letter")

    	# Number check
    	if re.search(r"\d", password):
        	checks_passed.append("Number")
    	else:
        	checks_failed.append("Number")

    	# Special character check
    	if re.search(r"[@$!%*?&#]", password):
        	checks_passed.append("Special character")
    	else:
        	checks_failed.append("Special character")

    	# Check against weak passwords list
    	try:
        with open("weaklist.txt", "r") as file:
            weak_passwords = {line.strip() for line in file}
        if password.lower() in (pw.lower() for pw in weak_passwords):
            checks_failed.append("Not found in weak password list")
        else:
            checks_passed.append("Not found in weak password list")
    	except FileNotFoundError:
        	print(Fore.YELLOW + "⚠️  Warning: weaklist.txt not found. Skipping weak password check.")
        	checks_passed.append("Weak password list (skipped)")

    	# Determine final verdict
    	if len(checks_failed) == 0:
        	verdict = Fore.GREEN + "✅ Strong password!"
    	elif len(checks_failed) <= 2:
        	verdict = Fore.YELLOW + "🟡 Moderate password."
    	else:
        	verdict = Fore.RED + "❌ Weak password."

    	# Display results
    	print("\n" + "="*40)
    	print(Fore.CYAN + "🔍 Password Strength Check Results")
    	print("="*40)

    	print(Fore.GREEN + "\n✔ Passed Checks:")
    	for check in checks_passed:
        	print(Fore.GREEN + f"  - {check}")

    	print(Fore.RED + "\n✖ Failed Checks:")
    	if checks_failed:
        	for check in checks_failed:
            	print(Fore.RED + f"  - {check}")
    	else:
        	print(Fore.GREEN + "  - None!")

    	print("\n" + verdict + Style.RESET_ALL)
    	print("="*40 + "\n")

7. Testing. Ran py file test functionality. In cmd,:

		python pass_checker.py

8. Using the password "123456789abcdefg", I tested that script, showing successful and unsuccessful passess against the scripted criteria. See below output:

<img width="633" height="321" alt="image" src="https://github.com/user-attachments/assets/3cbdb4a9-61a6-4aa7-8e5a-555598b2857b" />


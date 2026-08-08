import re

def check_password_strength(password):
    """
    Evaluates a password and returns its strength score and feedback.
    """
    # Initialize score and feedback list
    score = 0
    feedback = []

    # 1. Check length
    if len(password) >= 12:
        score += 2
    elif len(password) >= 8:
        score += 1
    else:
        feedback.append("Password is too short (minimum 8 characters required).")

    # 2. Check for lowercase letters
    if re.search(r"[a-z]", password):
        score += 1
    else:
        feedback.append("Add at least one lowercase letter (a-z).")

    # 3. Check for uppercase letters
    if re.search(r"[A-Z]", password):
        score += 1
    else:
        feedback.append("Add at least one uppercase letter (A-Z).")

    # 4. Check for digits
    if re.search(r"\d", password):
        score += 1
    else:
        feedback.append("Add at least one number (0-9).")

    # 5. Check for special characters
    if re.search(r"[!@#$%^&*(),.?\":{}|<>]", password):
        score += 1
    else:
        feedback.append("Add at least one special character (e.g., !, @, #, $, %).")

    # Determine strength category based on total score
    if score >= 6:
        strength = "Strong 💪"
    elif score >= 4:
        strength = "Medium ⚠️"
    else:
        strength = "Weak ❌"

    return strength, feedback

# --- Main Program Execution ---
if __name__ == "__main__":
    print("=== Password Strength Checker ===")
    user_password = input("Enter a password to test: ")
    
    # Run the validation
    rating, suggestions = check_password_strength(user_password)
    
    # Display results
    print(f"\nPassword Rating: {rating}")
    
    if suggestions:
        print("\nSuggestions to improve your password:")
        for tip in suggestions:
            print(f"- {tip}")
            

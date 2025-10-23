# URL
http://lafzk5oy.chals.mctf.io/

# Concept
Balance Desync + JWT-Controlled Balance on Return

# Method of solve   
Go to /signup, create an account (e.g., test@example.com  / password)
    1. Go to /login, log in
    2. Copy your JWT cookie (use browser dev tools)
    3. Go to /products, buy "Sesshōmaru" ($30)
    4. Restore the original JWT cookie (from step 3)
    5. Go to /profile, return the Sesshōmaru quote
        This will set your balance to $100 (from JWT) + $30 refund = $130
    6. Repeat steps 4-6 until balance ≥ $1000
        After 30 cycles: $100 + 30*30 = $1000
    7. Buy the "Flag" product
    8. Go to /profile — the flag will be displayed in your quotes
     


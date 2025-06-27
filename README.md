# Mini-Wallet
A simple command-line wallet sign-up system built with Haskell. Users can create wallets with unique usernames and passwords, demonstrating basic I/O, data handling, and user interaction in Haskell.

✅ TASK 1: DEFINE THE WALLET DATA Type
-- Define a Wallet type with username and password
data Wallet = Wallet {
    username :: String,
    password :: String
} deriving (Show, Eq)

✅ Task 2: Create a Sign-Up Function
Prompt the user for username and password, check if the username exists, and add to the list if not.

haskell
Copy
Edit
signUp :: [Wallet] -> IO [Wallet]
signUp existingWallets = do
    putStrLn "Enter a username:"
    u <- getLine
    if any (\w -> username w == u) existingWallets
        then do
            putStrLn "Username already exists. Try again."
            return existingWallets
        else do
            putStrLn "Enter a password:"
            p <- getLine
            let newWallet = Wallet u p
            putStrLn "Wallet created successfully!"
            return (newWallet : existingWallets)
            
✅ Task 3: Add a Main Menu
Loop over options until user quits.

haskell
Copy
Edit
mainMenu :: [Wallet] -> IO ()
mainMenu wallets = do
    putStrLn "\n=== Wallet Sign-Up Menu ==="
    putStrLn "1. Create Wallet"
    putStrLn "2. Exit"
    choice <- getLine
    case choice of
        "1" -> do
            newWallets <- signUp wallets
            mainMenu newWallets
        "2" -> putStrLn "Goodbye!"
        _   -> do
            putStrLn "Invalid option. Try again."
            mainMenu wallets
✅ Task 4: Entry Point
haskell
Copy
Edit
main :: IO ()
main = mainMenu []
🔧 Optional Stretch Goals
Save/load wallets to/from a file (Data.Aeson for JSON or simple writeFile).

Hash passwords using libraries like cryptohash.

Add login functionality.

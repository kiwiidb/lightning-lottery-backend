# lightning-lottery-backend
Backend for a lottery to win Amazon vouchers.

Project for the Lightning hackday 31/8/2018

For the wiki, see https://wiki.fulmo.org/index.php?title=Lightning_Lottery

This repository is for the backend code: communication with LND and storing of participants.
I plan on implementing this in Go.


This component needs to implement an API which listens for:

POST requests for new participants, and reply with an invoice to be paid.

The client can then create a websocket connection, on which the server will submit a message when the invoice is paid.

The participants need to be stored, and when a threshold is reached the following needs to happen:

Pick a participant at random.
Put him in the "winners database"
Delete all participants from the main database.
Buy voucher from BitRefill
Store voucher code in database with reference to winner.
E-mail the winner his code.

# Participant submission
For participant entering, the server should listen for a POST request on "/submit" which looks like:

{
    "e-mail": "someone@example.com",
    "voucher": "{steam},{amazon}" //type of voucher the participant wants to win
}

server will respond with the following response:

{
    "invoice": "lightning invoice",
    "paid": "false"
}
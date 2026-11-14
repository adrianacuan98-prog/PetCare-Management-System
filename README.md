# Pet Care Management System for Vets — Milestone 4

Flask CRUD web app for three existing Azure SQL tables: `Owner`, `Pet`, and `Appointment`.

## Mac setup

1. Install Python 3.11+ and Microsoft ODBC Driver 18 for SQL Server. On macOS with Homebrew: `brew install msodbcsql18` (Microsoft's tap and EULA acceptance may be needed; see Microsoft's official installation instructions).
2. Open Terminal in this folder.
3. Run `python3 -m venv .venv` and `source .venv/bin/activate`.
4. Run `pip install -r requirements.txt`.
5. Run `cp .env.example .env` and edit `.env` with your **application database user** and password (never commit this file). Use a database user with SELECT, INSERT, UPDATE and DELETE permissions on these tables. Do not use the grader account in published code.
6. Confirm Azure SQL firewall allows your computer's public IP and database is running.
7. Run `python app.py` and visit http://127.0.0.1:5000.

## Routes

- `/` — dashboard
- `/owners`, `/pets`, `/appointments` — list/read
- `/<resource>/new` — create
- `/<resource>/<id>/edit` — update
- `/<resource>/<id>/delete` — delete confirmation

## Schema assumptions to verify against Azure

The code follows the column names shown in Milestone 3: `Owner(OwnerID,Fname,Lname,PhoneNum,EAddress)`, `Pet(PetID,Bdate,Species,PetName,OwnerID,Breed)`, `Appointment(AppointmentID,PetID,VetID,AppointmentDate,AppointmentTime,Reason,Status)`, `Veterinarian(VetID,VetName)`. **Verify actual SQL column types and names** before testing; AppointmentTime may be a datetime column and the form sends ISO-style datetime. IDs are entered manually because the project sample tables show numbered IDs, but if IDs are `IDENTITY` columns remove them from INSERT and create forms.

## Test plan and screenshots

For EACH of Owners, Pets, Appointments: (1) show list, (2) fill create form, (3) show created row, (4) show edit form, (5) show updated row, (6) show delete confirmation, (7) show row removed. Use a test record with a unique ID. For FK demonstration, capture the Pet Owner drop-down and/or Appointment Pet/Veterinarian drop-down. Test FK-protected deletion of a referenced Owner or Pet, documenting the friendly error. **Do not delete real class data**.

## Security

SQL values use bound `?` parameters; only hardcoded allowlisted table and column names are interpolated. `.env` is excluded from Git. For local classroom use; add authentication, CSRF protection, and production server before public deployment. `FLASK_DEBUG=1` is local-only.

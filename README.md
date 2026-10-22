# Server Awards - Discord Voting App

Moderní a rychlá aplikace pro týdenní a měsíční hlasování mezi přáteli na serveru.

---

## Předdefinovaní členové a administrace

- **Kandidáti (nominovaní):** Michcal, Rada, Chulio, Sweedy, Jana, Viky, Fejtas, Séba, Sikyta
- **Administrátorský účet:**
  - Uživatelské jméno: `admin`
  - Heslo: `mike@6769`
- **Kategorie:** 6 týdenních + 2 měsíční
- **Bezpečnost:** Hlasovat mohou pouze přihlášení uživatelé. Admin panel (`/admin`) je přístupný pouze pro účet `admin`.

---

## 1. Odeslání projektu na GitHub

Otevřete terminál (PowerShell) ve složce projektu a spusťte:

```bash
git init
git add .
git commit -m "Initial commit"
git branch -M main
git remote add origin https://github.com/VASE_JMENO/NAZEV_REPOZITARE.git
git push -u origin main
```

---

## 2. Nasazení na Vercel

1. Otevřete [Vercel](https://vercel.com) a přihlaste se přes GitHub.
2. Klikněte na **Add New...** -> **Project**.
3. Vyberte váš repozitář z GitHubu a klikněte na **Import**.
4. Přejděte na sekci **Environment Variables** a přidejte proměnné (viz níže).
5. Klikněte na **Deploy**.

---

## 3. Nastavení databáze (Vercel Postgres nebo Neon)

Protože Vercel používá bezserverové prostředí, aplikace používá PostgreSQL.

### Možnost A: Vercel Postgres (nejjednodušší)
1. V dashboardu projektu na Vercelu klikněte na záložku **Storage**.
2. Klikněte na **Create Database** -> vyberte **Postgres**.
3. Propojte databázi s vaším projektem (**Connect to Project**).
4. Vercel automaticky vyplní proměnnou `DATABASE_URL` do nastavení projektu.

### Možnost B: Neon.tech (zdarma na 1 kliknutí)
1. Zaregistrujte se na [Neon.tech](https://neon.tech) a vytvořte bezplatnou PostgreSQL databázi.
2. Zkopírujte Connection String (`postgresql://...`).
3. Vložte jej do Vercel Environment Variables jako `DATABASE_URL`.

---

## 4. Proměnné prostředí na Vercelu (Environment Variables)

V nastavení projektu na Vercelu (**Settings -> Environment Variables**) nastavte:

| Název proměnné | Hodnota |
| --- | --- |
| `DATABASE_URL` | Vaše PostgreSQL URL (z Vercel Postgres nebo Neon) |
| `AUTH_SECRET` | Libovolný tajný klíč o délce min. 32 znaků (např. `super-secret-key-voting-app-32chars`) |
| `NEXTAUTH_SECRET` | Stejná hodnota jako u `AUTH_SECRET` |

---

## 5. Inicializace databáze po nasazení

Po vytvoření PostgreSQL databáze stačí jednou inicializovat tabulky a výchozího správce:

1. Ve svém lokálním souboru `.env` dočasně nastavte `DATABASE_URL` na vaši Vercel/Neon PostgreSQL adresu.
2. V terminálu spusťte:

```bash
npx prisma db push
npx tsx prisma/seed.ts
```

Tím se vytvoří všechny tabulky, administrátorský účet `admin` / `mike@6769`, 9 členů a kategorie.

---

## Lokální vývoj na počítači

Pro lokální spuštění na Windows stačí dvakrát kliknout na `start.bat` nebo spustit:

```bash
npm run dev
```

Aplikace běží na `http://localhost:3000`.

### Přepínání databáze pro vývoj
- Pro lokální testování s SQLite: `npm run db:use-sqlite`
- Pro nasazení na Vercel s PostgreSQL: `npm run db:use-postgres`

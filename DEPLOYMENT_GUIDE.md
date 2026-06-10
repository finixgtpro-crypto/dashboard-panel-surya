# Panduan Deployment ke Vercel

## Siap untuk Production

Aplikasi sudah dilengkapi dengan:
- ✅ Authentication (Login/Register)
- ✅ Protected Dashboard
- ✅ Responsive Design
- ✅ Real-time Data Updates
- ✅ Production Build tested

## Langkah-Langkah Deployment

### 1. Setup GitHub Repository

```bash
# Pastikan kode sudah di-commit
git add .
git commit -m "Add login authentication and prepare for deployment"
git push origin main
```

### 2. Buat Vercel Account & Deploy

**Opsi A: Via Vercel Dashboard (PALING MUDAH)**

1. Buka https://vercel.com
2. Klik "Sign Up" → Login dengan GitHub
3. Klik "Import Project"
4. Pilih repository ini
5. Vercel auto-detect Vite config
6. Klik "Deploy"

**Opsi B: Vercel CLI**

```bash
npm install -g vercel
vercel
```

### 3. Setup Environment Variables

**Di Vercel Dashboard:**

1. Buka project yang sudah di-deploy
2. Settings → Environment Variables
3. Tambah 2 variables:

```
VITE_SUPABASE_URL = [copy dari .env lokal]
VITE_SUPABASE_ANON_KEY = [copy dari .env lokal]
```

4. Redeploy project (automatic setelah add env vars)

### 4. Test Login

Setelah deployed:

1. Buka URL Vercel (misal: `https://solartrack.vercel.app`)
2. Klik "Daftar"
3. Input email & password baru
4. Klik "Daftar"
5. Klik "Masuk"
6. Input email & password yang tadi
7. Dashboard muncul = SUCCESS!

## Environment Variables

File `.env` harus contain:

```
VITE_SUPABASE_URL=https://xxxxx.supabase.co
VITE_SUPABASE_ANON_KEY=eyJhbGc...
```

**JANGAN push `.env` ke GitHub!** (sudah di `.gitignore`)

## Fitur Authentication

- Daftar akun baru dengan email & password
- Login dengan akun yang sudah terdaftar
- Data disimpan di Supabase `auth.users` table
- Password di-encrypt dengan bcrypt
- Session management otomatis
- Logout button di header

## File-File Penting

- `src/components/LoginPage.tsx` - UI Login/Register
- `src/App.tsx` - Auth state management
- `src/lib/supabase.ts` - Supabase client config
- `src/hooks/useSolarData.ts` - Real-time data subscription
- `supabase/migrations/` - Database schema

## Troubleshooting

### Build Error
```bash
npm install
npm run build
```

### Environment Variables Tidak Terbaca
- Double-check di Vercel Dashboard
- Redeploy setelah add env vars
- Check console log di browser (DevTools)

### Database Connection Error
- Pastikan Supabase project active
- Check VITE_SUPABASE_URL dan VITE_SUPABASE_ANON_KEY
- Test local dengan `npm run dev` dulu

### Login Tidak Berfungsi
- Check browser DevTools Console
- Verify email & password benar
- Clear browser cache

## Deploy Otomatis

Setiap push ke branch main, Vercel otomatis:
1. Build project
2. Run tests (jika ada)
3. Deploy ke production
4. Update URL live

## Domain Custom

1. Di Vercel Dashboard → Settings
2. Domains
3. Tambah domain custom
4. Update DNS records sesuai instruksi

## Support

- Vercel Docs: https://vercel.com/docs
- Supabase Docs: https://supabase.com/docs
- React Vite: https://vitejs.dev

# Pronto Digital

Sistema de prontuário clínico e educacional com planos psicopedagógicos.

## Stack
- HTML + CSS + JavaScript (SPA)
- [Supabase](https://supabase.com) (banco de dados)
- [Vercel](https://vercel.com) (hospedagem)

## Banco de Dados (Supabase)

Execute o SQL abaixo no Supabase SQL Editor para criar as tabelas:

```sql
CREATE TABLE IF NOT EXISTS records (
  id UUID DEFAULT gen_random_uuid() PRIMARY KEY,
  category TEXT NOT NULL,
  name TEXT NOT NULL,
  date TEXT,
  contact TEXT,
  institution TEXT,
  history TEXT,
  goals TEXT,
  strategies TEXT,
  created_at TIMESTAMPTZ DEFAULT NOW()
);

CREATE TABLE IF NOT EXISTS daily_notes (
  id UUID DEFAULT gen_random_uuid() PRIMARY KEY,
  record_id UUID REFERENCES records(id) ON DELETE CASCADE,
  date TEXT,
  title TEXT,
  content TEXT NOT NULL,
  created_at TIMESTAMPTZ DEFAULT NOW()
);

ALTER TABLE records ENABLE ROW LEVEL SECURITY;
ALTER TABLE daily_notes ENABLE ROW LEVEL SECURITY;

CREATE POLICY "Allow all for anon on records" ON records FOR ALL TO anon USING (true) WITH CHECK (true);
CREATE POLICY "Allow all for anon on daily_notes" ON daily_notes FOR ALL TO anon USING (true) WITH CHECK (true);
```

## Deploy

1. Push para GitHub
2. Conectar repositório na [Vercel](https://vercel.com)
3. Deploy automático a cada push

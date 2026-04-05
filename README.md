# D.PRO Financial Control

מערכת ניהול פיננסי עם סנכרון בין מכשירים.

## עדכון — חיבור Supabase לסנכרון

### שלב 1: צור פרויקט Supabase (חינם)
1. לך ל-[supabase.com](https://supabase.com) ולחץ Start your project
2. התחבר עם GitHub
3. לחץ New Project
4. שם: `dpro-finance`
5. סיסמה: בחר סיסמה חזקה (שמור אותה)
6. Region: בחר הכי קרוב (Central EU)
7. לחץ Create new project — תחכה דקה

### שלב 2: צור טבלה
1. בתפריט השמאלי לחץ **SQL Editor**
2. לחץ **New query**
3. העתק-הדבק את הטקסט הבא ולחץ **Run**:

```sql
CREATE TABLE IF NOT EXISTS entries (
  id TEXT PRIMARY KEY,
  type TEXT NOT NULL,
  subcategory TEXT NOT NULL,
  amount NUMERIC NOT NULL DEFAULT 0,
  date TEXT NOT NULL,
  description TEXT DEFAULT '',
  client TEXT DEFAULT '',
  created_at TIMESTAMP WITH TIME ZONE DEFAULT NOW()
);

ALTER TABLE entries DISABLE ROW LEVEL SECURITY;

CREATE INDEX IF NOT EXISTS idx_entries_date ON entries (date DESC);
CREATE INDEX IF NOT EXISTS idx_entries_type ON entries (type);
```

4. צריך לראות "Success"

### שלב 3: העתק מפתחות
1. לחץ **Connect** (כפתור ירוק למעלה)
2. בחר **App Frameworks**
3. תראה `NEXT_PUBLIC_SUPABASE_URL` ו-`NEXT_PUBLIC_SUPABASE_PUBLISHABLE_KEY`
4. העתק את שניהם

### שלב 4: הוסף מפתחות ל-Vercel
1. לך ל-Vercel → הפרויקט שלך → **Settings** → **Environment Variables**
2. הוסף:
   - Name: `NEXT_PUBLIC_SUPABASE_URL` → Value: הכתובת מסופאבייס
   - Name: `NEXT_PUBLIC_SUPABASE_ANON_KEY` → Value: המפתח מסופאבייס
3. לחץ Save

### שלב 5: העלה קוד מעודכן ל-GitHub
1. החלף את הקבצים ב-GitHub repo עם הקבצים החדשים
2. Vercel יבנה מחדש אוטומטית

### שלב 6: בדוק
1. פתח את האפליקציה
2. ליד "FINANCIAL CONTROL" תראה נקודה:
   - 🟢 ירוק = מסונכרן
   - 🟠 כתום = מסנכרן
   - 🔴 אדום = לא מחובר
3. הוסף רשומה באייפון — תראה אותה באייפד תוך שניות (רענן)

# צ׳ק ליסט הריון לפי שבועות

אתר סטטי (`index.html` אחד, Firebase דרך CDN) עם משימות, בדיקות, תורים וזכויות לפי שבועות ההריון, לפי מסלול המעקב בישראל.

- התחברות עם Google (Firebase Auth)
- משפחה משותפת: קישור הזמנה `?join=` או הזמנה לפי אימייל
- רשימה משותפת בזמן אמת (Firestore): תאריך, קופה, סימונים ומשימות אישיות

## מבנה הנתונים
- `users/{uid}`: name, email, avatar, familyId
- `families/{fid}`: name, members[]
- `families/{fid}/data/settings`: mode, date, kupa
- `families/{fid}/data/done`: items.{taskId} = { by, at }
- `families/{fid}/tasks/{id}`: w, t, d, by
- `invites/{email}`: familyId, invitedBy

## הגדרות ב-Firebase
1. Authentication → Sign-in method → Google: Enable
2. Authentication → Settings → Authorized domains: להוסיף את דומיין ה-Vercel
3. Firestore Database: ליצור מסד, ולהדביק את `firestore.rules` בלשונית Rules
4. Google Cloud Console → Credentials → OAuth client (Web): להוסיף Authorized redirect URI
   `https://<vercel-domain>/__/auth/handler` (נדרש להתחברות באייפון דרך ה-proxy שב-`vercel.json`)

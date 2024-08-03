# Amplify Next.js Example
This is an example of how to use Amplify with Next.js.

## Prerequisites
- Node.js
- npm
- AWS Account
- AWS CLI

Make sure you have the AWS CLI installed and configured with your AWS account. For example, you can export your AWS credentials as environment variables:
```bash
export AWS_ACCESS_KEY_ID=...
export AWS_SECRET_ACCESS_KEY=...
export AWS_SESSION_TOKEN=...
```

## Getting Started
1. Create a new Next.js app
```bash
npx create-next-app@latest amplify-nextjs
```

2. Change into the new app directory
```bash
cd amplify-nextjs
```

3. Install dependencies
```bash
npm add --save-dev @aws-amplify/backend@latest @aws-amplify/backend-cli@latest typescript
```

4. Next, create the entry point for your backend, `amplify/backend.ts`, with the following code:
```typescript
import { defineBackend } from '@aws-amplify/backend';
// import { auth } from './auth/resource';

defineBackend({
  // auth,
});

// Uncomment auth if auth is defined in auth/resource
```

5. You can use define* functions to define your resources. For example, you can define authentication:
```typescript
import { defineAuth } from '@aws-amplify/backend';

export const auth = defineAuth({
  loginWith: {
    email: true
  }
});
```

6. Now you can create your backend by running the following command, this will create `amplify_outputs.json` inside `src/app` directory:
```bash
npx ampx sandbox --outputs-out-dir=src/app
```

6. Connect your app to the backend by adding the following code to `src/app/page.tsx`:
```tsx
"use client";

import { Amplify } from 'aws-amplify';
import outputs from "./amplify_outputs.json";

// Use Authenticator library to handle authentication logic and UI
import { Authenticator } from '@aws-amplify/ui-react';
import '@aws-amplify/ui-react/styles.css';

Amplify.configure(outputs);

export default function Home() {
  return (
    <Authenticator>
      {({ signOut, user }) => (
        <main className="...">
          ...
        </main>
      )}
    </Authenticator>
  );
}
```

7. Run your app
```bash
npm run dev
```

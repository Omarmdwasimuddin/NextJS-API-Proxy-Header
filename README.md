## NextJS API---> Working With Request Header In Proxy

### Get header properties value.
![](https://imgur.com/icCqQ3x.png)
![](https://imgur.com/gubrNX5.png)

```bash
import { NextRequest, NextResponse } from "next/server";


export function proxy(request: NextRequest) {
    if (request.nextUrl.pathname.startsWith('/api')) {
        const requestHeader = new Headers(request.headers);
        const token = requestHeader.get('token');

        if (token === 'xyz-123-abc-000') {
            return NextResponse.next();
        }else {
            return NextResponse.json(
                {status: "fail"},
                {status: 401}
            )
        }
    }
}
```

```bash
import { NextResponse, NextRequest } from "next/server";


export async function GET(request:NextRequest) {

    
    return NextResponse.json(
        {status: "success", message: "request success"},
        {status: 200}
    )
}
```
---

### Set header properties value.
![](https://imgur.com/HUZCy5E.png)

```bash
import { NextRequest, NextResponse } from "next/server";


export function proxy(request: NextRequest) {
    if (request.nextUrl.pathname.startsWith('/api')) {
        const requestHeader = new Headers(request.headers);
        requestHeader.set('user_id','001135');

        return NextResponse.next(
            { request: { headers:requestHeader } }
        );
    }
}
```

```bash
import { headers } from "next/headers";
import { NextResponse, NextRequest } from "next/server";


export async function GET(request:NextRequest) {

    const headerList = headers();
    const userId = (await headerList).get('user_id');

    return NextResponse.json(
        {status: "success", message: userId},
        {status: 200}
    )
}
```
---

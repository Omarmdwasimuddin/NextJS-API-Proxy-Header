## NextJS API---> Working With Request Header In Proxy

###
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

---
id: title
title: Angular Title
---

`app.module.ts`

```ts
import { Title } from '@angular/platform-browser';

  providers: [Title],
```

`app.component.ts`

```ts
import { Component, OnInit } from "@angular/core";
import { Router, NavigationEnd, ActivatedRoute } from "@angular/router";
import { Title } from "@angular/platform-browser";
import { filter, map, mergeMap } from "rxjs/operators";

@Component({
  selector: "app-root",
  template: `
    <router-outlet></router-outlet>
  `,
  styles: []
})
export class AppComponent implements OnInit {
  constructor(
    private router: Router,
    private activatedRoute: ActivatedRoute,
    private titleService: Title
  ) {}

  ngOnInit() {
    this.router.events
      .pipe(
        filter(event => event instanceof NavigationEnd),
        map(() => this.activatedRoute),
        map(route => {
          while (route.firstChild) route = route.firstChild;
          return route;
        }),
        filter(route => route.outlet === "primary"),
        mergeMap(route => route.data)
      )
      .subscribe(event => {
        this.titleService.setTitle(
          event["title"] ? event["title"] : "default title"
        );
      });
  }
}
```

`***-routing.module.ts`

```ts
const routes: Routes = [
  {
    path: "discounts",
    component: DiscountsComponent,
    data: { title: "用户折扣管理" }
  }
];
```

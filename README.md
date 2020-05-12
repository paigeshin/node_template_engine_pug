# node_express_basic

# Pug

- Installation

```jsx
//Global Configuration
app.set('view engine', 'pug');
app.set('views', 'views');
```

`app.set` 은 global configuration을 의미한다. 

- pug basic syntax

```jsx
<!DOCTYPE html>
html(lang='en')
    head
        meta(charset='UTF-8')
        meta(name='viewport', content='width=device-width, initial-scale=1.0')
        meta(http-equiv='X-UA-Compatible', content='ie=edge')
        title #{docTitle}
        link(rel='stylesheet', href='/css/main.css')
        link(rel='stylesheet', href='/css/product.css')
    body
        header.main-header
            nav.main-header__nav
                ul.main-header__item-list
                    li.main-header__item
                        a.active(href="/") Shop
                    li.main-header__item
                        a.active(href="/admin/add-product") Add Product
        main
            if prods.length > 0
                .grid
                    each product in prods
                        //-
                            prods를 서버에서 받아와서 for each 문을 돌린다.
                        article.card.product-item
                            header.card__header
                                h1.product__title #{product.title}
                            div.card__image
                                img(src="https://pbs.twimg.com/media/EKkxRz1U4AASYK7.jpg" alt="")
                            div.card__content
                                h2.product__price $19.99
                                p.product__description A very interesting book about so many even more interesting things!
                            .card__actions
                                button.btn Add to Cart
            else
                h1 No Products
```

⇒ content 가 없다면 div를 적어줘야하지만, 안에 content가 있다면 `div` 를 적어줘야 한다.

⇒ data 가져오기 `#{key}`

- header, footer, `main-layout.png`

```jsx
<!DOCTYPE html>
html(lang="en")
    head
        meta(charset="UTF-8")
        meta(name="viewport", content="width=device-width, initial-scale=1.0")
        meta(http-equiv="X-UA-Compatible", content="ie=edge")
        title #{pageTitle}
        link(rel="stylesheet", href="/css/main.css")
        block styles
    body
        header.main-header
            nav.main-header__nav
                ul.main-header__item-list
                    li.main-header__item
                        a(href="/", class=(path === '/' ? 'active' : '')) Shop
                    li.main-header__item
                        a(href="/admin/add-product", class=(path === '/admin/add-product' ? 'active' : '')) Add Product
        block content
```

- `404.pug`

```jsx
extends layouts/main-layout.pug

block content
    h1 Page Not Found!
```

- `add-product.pug`

```jsx
extends layouts/main-layout.pug

block styles
    link(rel="stylesheet", href="/css/forms.css")
    link(rel="stylesheet", href="/css/product.css")

block content
    main
        form.product-form(action="/admin/add-product", method="POST")
            .form-control
                label(for="title") Title
                input(type="text", name="title")#title
            button.btn(type="submit") Add Product
```

- `shop.pug`

```jsx
extends layouts/main-layout.pug

block styles
    link(rel="stylesheet", href="/css/product.css")

block content
    main
        if prods.length > 0
            .grid
                each product in prods
                    article.card.product-item
                        header.card__header
                            h1.product__title #{product.title}
                        div.card__image
                            img(src="data:image", alt="A Book")
                        div.card__content
                            h2.product__price $19.99
                            p.product__description A very interesting book about so many even more interesting things!
                        .card__actions
                            button.btn Add to Cart
        else
            h1 No Products
```

- express, render method argument `path`

```jsx
res.render('add-product', { pageTitle: 'Add Product', path: '/admin/add-product' });
```

### 개념정리

- extend를 이용해서 파일을 가져옴
- block 을 이용해서 code 작성
- 기본적으로 indent를 사용하여 코드를 작성한다.
- key 값으로 받아온 데이터들은 #{key} 형식으로 받아옴
- `foreach` 사용법 - `each product in prods`
- path를 이용해서 css를 control 할 수 있다.

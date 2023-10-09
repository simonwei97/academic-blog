---
title: Hugo 测试
subtitle: Welcome 👋 We know that first impressions are important, so we've populated your new site with some initial content to help you get familiar with everything in no time.

# Summary for listings and search engines
summary: Welcome 👋 We know that first impressions are important, so we've populated your new site with some initial content to help you get familiar with everything in no time.

# Link this post with a project
projects: []

# Date published
date: "2020-12-13T00:00:00Z"

# Date updated
lastmod: "2020-12-13T00:00:00Z"

# Is this an unpublished draft?
draft: false

# Show this page in the Featured widget?
featured: false

# Featured image
# Place an image named `featured.jpg/png` in this page's folder and customize its options here.
image:
  caption: "Image credit: [**xxx**](https://unsplash.com/photos/CpkOjOcXdUY)"
  focal_point: ""
  placement: 1
  preview_only: false

# banner:
# image: "page-title.jpg"
# caption: "Image credit: [**Geo**](https://unsplash.com/photos/CpkOjOcXdUY)"

authors:
  - admin

tags:
  - Academic
  - 开源

categories:
  - Demo
  - 教程
# Book page type (do not modify).
# type: book

toc: true
---

```python
import libr
print('hello')
```

```rust
mod back_of_house {
    pub struct Breakfast {
        pub toast: String,
        seasonal_fruit: String,
    }

    impl Breakfast {
        pub fn summer(toast: &str) -> Breakfast {
            Breakfast {
                toast: String::from(toast),
                seasonal_fruit: String::from("peaches"),
            }
        }
    }
}
pub fn eat_at_restaurant() {
    let mut meal = back_of_house::Breakfast::summer("Rye");
    meal.toast = String::from("Wheat");
    println!("I'd like {} toast please", meal.toast);
}
fn main() {
    eat_at_restaurant()
}
```

## 概括

```go
package main

import "fmt"

func main() {
   var sum int = 17
   var count int = 5
   var mean float32

   mean = float32(sum)/float32(count)
   fmt.Printf("mean 的值为: %f\n",mean)
}

```

{{< math >}}

$$
y = \sqrt {x_1^2 + x_2^2 + x_3^2 + x_4^2}
$$

{{< /math >}}

{{< math >}}

$$
\gamma_{n} = \frac{ \left | \left (\mathbf x_{n} - \mathbf x_{n-1} \right )^T \left [\nabla F (\mathbf x_{n}) - \nabla F (\mathbf x_{n-1}) \right ] \right |}{\left \|\nabla F(\mathbf{x}_{n}) - \nabla F(\mathbf{x}_{n-1}) \right \|^2}
$$

{{< /math >}}

{{< math >}}

$$
f(k;p_{0}^{*}) = \begin{cases}p_{0}^{*} & \text{if }k=1, \\
1-p_{0}^{*} & \text{if }k=0.\end{cases}
$$

{{< /math >}}

{{% callout note %}}
A Markdown callout is useful for displaying notices, hints, or definitions to your readers.
{{% /callout %}}

{{% callout warning %}}
Here's some important information...
{{% /callout %}}

| No  | 机构 | 计划 | 备注 | 负责人 |
| --- | ---- | ---- | ---- | ------ |
| 1   | A    |      |      |        |
| 2   | B    |      |      |        |
| 3   | C    |      |      |        |

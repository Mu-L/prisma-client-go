# Prisma Data Proxy

Connection limit issues got you down? By using Prisma's Data Proxy, you can pool your connections to avoid overloading your database. You can also make use of a web data browser and builtin query console at [our Cloud platform](https://cloud.prisma.io).

![](https://camo.githubusercontent.com/21dd928a8dffd6f4f4de5bdc37def39e1867967b6deff8bc34c96ef563afe127/68747470733a2f2f73332e75732d776573742d322e616d617a6f6e6177732e636f6d2f7365637572652e6e6f74696f6e2d7374617469632e636f6d2f34633531323735392d663031652d343335652d623738352d3332613035646261663331632f436c65616e53686f745f323032312d31312d30315f61745f31382e33332e323832782e706e673f582d416d7a2d416c676f726974686d3d415753342d484d41432d53484132353626582d416d7a2d43726564656e7469616c3d414b49415437334c324734354f334b5335325935253246323032313131303225324675732d776573742d322532467333253246617773345f7265717565737426582d416d7a2d446174653d3230323131313032543132343033345a26582d416d7a2d457870697265733d383634303026582d416d7a2d5369676e61747572653d3261613930386266363438356462363465326332643731633864386164623063356264356632353265646135313032326434353830373138636464313238333726582d416d7a2d5369676e6564486561646572733d686f737426726573706f6e73652d636f6e74656e742d646973706f736974696f6e3d66696c656e616d65253230253344253232436c65616e53686f742532353230323032312d31312d303125323532306174253235323031382e33332e3238253235343032782e706e67253232)

First, enable the data proxy preview feature in your prisma.schema:

```diff
generator client {
  provider        = "go run github.com/prisma/prisma-client-go"
+ previewFeatures = ["dataProxy"]
}
```

You can generate a "Data Proxy"-enabled Go Client in the Prisma schema or individually using an env var.
If you want to use the data proxy everywhere, you might want to set it in the schema, whereas when you just
want to use the data proxy in production, you might want to set an env var in your deployment script.

Setting it in the schema:

```diff
generator client {
  provider        = "go run github.com/prisma/prisma-client-go"
  previewFeatures = ["dataProxy"]
+ engineType      = "dataproxy"
}
```

Setting it just once when generating the client:

```
PRISMA_CLIENT_ENGINE_TYPE='dataproxy' go run github.com/prisma/prisma-client-go generate
```

Then you can use the Go client as you would normally. There won't be any generated query engine files as opposed to the normal mode.

For more information and caveats, read the full [Prisma Data Proxy docs](https://www.prisma.io/docs/concepts/components/prisma-data-platform#prisma-data-proxy).

### httpmock
---
https://github.com/jarcoal/httpmock

```go
import "github.com/jarcoal/httpmock"

func TestFetchArticles(t *testing.T) {
  httpmock.Activate()
  defer httpmock.DeactivateAndReset()
  httpmock.RegisterREsponder("GET", "https://api.mybiz.com/articles.json")
    httpmock.newStringResponder(200, `[{"id": 1, "name": "My Great Article"}]`)
    
  httpmock.GetTotalCallCount()
  
  info := httpmock.GetCallCountInfo()
  info["GET https://api.mybiz.com/articles.json"]
}


























// article_suite_test.go
import (
  "github.com/jarcoal/httpmock"
  "github.com/go-resty/resty"
)

var _ = BeforeSuite(func() {
  httpmock.ActivateNonDefault(resty.DefaultClient.GetClient())
})

var _ = BeforeEach(func() {
  httpmock.Reset()
})

var _ = AfterSuite(func() {
  httpmock.DeactivateAndReset()
})

// article_test.go
import (
   "github.com/jarcoal/httpmock"
   "github.com/go-resty/resty"
)

var _ = Describe("Articles", func() {
  It("returns a list of articles", func() {
    fixture := `{"status":{"message": "Your message", "code": 200}}`
    responder, err := httpmock.NewJsonResponder(200, fixture)
    fakeUrl := ""
    httpmock.RegisterResponder("GET", fakeUrl, responder)
    
    articleObject := &models.Article{}
    _, err := resty.R().SetResult(articleObject).Get(fakeUrl)
  })
})

```

```
go get github.com/jarcoal/httpmock
```

```
```



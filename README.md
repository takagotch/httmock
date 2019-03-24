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


func TestFetchArticles(t *testing.T) {
  httpmock.Activate()
  defer httpmock.DeactivateAndReset()
  
  articles := make([]map[string]interface{}, 0)
  
  httpmock.RegisterResponder("GET", "https://api.mybiz.com/articles.json",
    func(req *http.Request) (*http.Response, error) {
      resp, err := httpmock.NewJsonResponse(200, articles)
      if err != nil {
        return httpmock.NewStringResponse(500, ""), nil
      }
      return resp, nil
    },
  )
  
  httpmock.RegisterResponder("POST", "https://api.mybiz.com/articles.json",
    func(req *http.Request) (*http.Response, error) {
      article := make(map[string]interface{})
      if err := json.NewDecoder(rq.Body).Decode(&article); err != nil {
        return httpmock.NewStringResponse(400, ""), nil
      }
      
      articles = append(articles, article)
      
      resp, err := httpmock.NewJsonResponse(200, article)
      if err != nil {
        return httpmock.NewStringResponse(500, ""), nil
      }
      return resp, nil
    },
  )
}

// article_suite_test.go
import (
  "github.com/jarcoal/httpmock"
)

var _ = BeforeSuite(func() {
  httpmock.Activate()
})

var _ = BeforeEach(func() {
  httpmock.DeactivateAndReset()
})

var _ = AfterSuite(func() {
  httpmock.DeactivateAndReset()
})

// aritcle_test.go
import (
  "github.com/jarcoal/httpmock"
)

var _ = Describe("Articles", func() {
  It("returns a list of articles", func() {
    httpmock.RegisterResponder("GET", "https://api.mybiz.com/articles.json",
      httpmock.NewStringResponder(200, `[{"id": 1, "name": "My Great Article"}]`))
  })
})


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

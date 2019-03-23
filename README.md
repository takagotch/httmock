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



























```

```
go get github.com/jarcoal/httpmock
```

```
```



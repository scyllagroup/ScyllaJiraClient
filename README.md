# ScyllaJiraClient
Custom Jira Client

```
ScyllaJiraClient client = new ScyllaJiraClient("username", "password");

// List project ids and keys...
client.Projects.GetProjects().ForEach(proj => { Console.WriteLine(string.Format("{0}-{1}", proj.id, proj.key)); });

// TYPED - Grab an issue
Issue issue = client.Issues.GetIssueByKey("BAE-15");

// JSON - Grab an issue
IRestResponse issue2 = client.Execute(new RestRequest("issue/BAE-15"));
string json = issue2.Content;

// Create issue
CreateIssueResponse issue3 = client.Issues.CreateIssue("AT", "First Issue", "Description of the issue...");

// Find all worklog entries
result.issues.ForEach(issue => {
  WorkLogResponse resp = client.Issues.GetIssueWorklogs(issue.key);
  if (resp.total > 0) 
  {
    Console.WriteLine(issue.key + " - " + issue.fields.summary);
    resp.worklogs.ForEach(wl => {
      Console.WriteLine("\t" + wl.author.displayName + " spent " + wl.timeSpent + " on " + wl.created.ToShortDateString());
    });
  }
});
```

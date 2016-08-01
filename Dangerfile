# Ensure there is a summary for a pull request
fail 'Please provide a summary in the Pull Request description' if github.pr_body.length < 5

# Warn when there are merge commits in the diff
warn 'Please rebase to get rid of the merge commits in this Pull Request' if git.commits.any? { |c| c.message =~ /^Merge branch 'master'/ }

# Only one library per pull request
warn 'Please only add one library per Pull Request' if git.lines_of_code > 1

# Warn if pull request is not updated
warn 'Please update the Pull Request title' if github.pr_title.include? 'Update README.md'

# Check links
require 'json'
results = File.read 'ab-results-README.md.json'
j = JSON.parse results
issues = j['issues']
unless issues.nil?
  fail 'Found links issues'
  message = "#### Link issues by [`awesome_bot`](https://github.com/dkhamsing/awesome_bot)\n\n"
  message << "Line | Status | Link\n"
  message << "| --- | --- | --- |\n"

  issues.each do |i|
    message << "#{i['loc']} | #{i['status']} | #{i['url']}"
  end
  markdown message
end

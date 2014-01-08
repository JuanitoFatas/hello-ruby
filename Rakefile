require File.dirname(__FILE__) + "/github-emojis"

## m for message
# rake m README.md
# rake m "Update Guides." README.md
desc "Write a custom commit message then push to GitHub."
task :m do
  file_name = ARGV.last
  message   = ARGV[-1*(ARGV.length-1)]

  deploy(file_name, message: message)
  task message.to_sym   do ; end
  task file_name.to_sym do ; end
end

##
# Deploy to GitHub.
def deploy(file_name, **opts)
  message = if opts[:message].nil?
              template % { msg: file_name }
            else
              template % { msg: opts[:message] }
            end

  git_add_commit_push! file_name, message

  puts "\nDeploy to GitHub complete :)"
end

def git_add_commit_push!(file_name, message)
  system "git add #{file_name}"
  system "git commit -m \"#{message}\""
  system "git push origin gh-pages"
end

def template
  [ %Q<#{rand_emojis} %{msg} #{rand_emojis}>,
    %Q<%{msg} #{rand_emojis}>,
    %Q<#{rand_emojis} %{msg}> ].sample
end

def rand_emojis
  GITHUB_EMOJIS.sample
end

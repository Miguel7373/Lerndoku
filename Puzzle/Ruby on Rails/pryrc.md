```rb
# 1. ALLGEMEINE EINSTELLUNGEN
Pry.config.editor = 'nano'

# 2. PROMPT PERSONALISIERUNG
require 'reline'
Object.const_set(:Readline, Reline) unless defined?(Readline)

Pry.config.prompt = Pry::Prompt.new(
  "rails_hacker",
  "Ein cooler, informativer Rails Prompt",
  [
    proc do |target_self, nest_level, pry, sep|
      project = defined?(Rails) ? Rails.application.class.name.split('::').first : File.basename(Dir.pwd)

      env = defined?(Rails) ? Rails.env : "ruby"

      c_project = "\e[38;5;39m"
      c_env     = env == 'production' ? "\e[1;31m" : "\e[38;5;114m"
      c_ruby    = "\e[38;5;208m"
      c_reset   = "\e[0m"

      nest = nest_level > 0 ? " \e[33m(level:#{nest_level})\e[0m" : ""

      "[#{c_project}#{project}#{c_reset}][#{c_env}#{env}#{c_reset}] #{c_ruby}â™¦ï¸ #{RUBY_VERSION}#{c_reset}#{nest}#{sep} "
    end,

    proc do |target_self, nest_level, pry|
      "  \e[38;5;239mâžœ\e[0m "
    end
  ]
)

# 3. ALIASE
Pry.commands.alias_command 'c', 'continue'
Pry.commands.alias_command 'f', 'finish'
Pry.commands.alias_command 'u', 'up'
Pry.commands.alias_command 'd', 'down'
Pry.commands.alias_command 's', 'step'
Pry.commands.alias_command 'n', 'next'
Pry.commands.alias_command 'q', 'exit'
Pry.commands.alias_command 'clear', 'clear-screen'

# 4. FORMATIERUNG (AMAZING PRINT)
begin
  require 'amazing_print'

  AmazingPrint.pry!

  AmazingPrint.defaults = {
    indent:        -2,
    index:         true,
    limit:         10,
    ruby19_syntax: true,
    sort_keys:     true,
    color: {
      string:     :cyan,
      symbol:     :yellow,
      integer:    :green,
      float:      :green,

      trueclass:  :green,
      falseclass: :red,
      nilclass:   :red
    }
  }
rescue LoadError
end
````


### Pry Configuration (`.pryrc`)

The Pryrc is plain Ruby code, so you can add any function you like to it.

The `.pryrc` can be in your user directory and still work in every project. Just keep in mind that the `.pryrc` in a project will always have priority.

The `.pryrc` normally contains aliases and useful functions to navigate your debugger, as well as configuration for Pry gems.
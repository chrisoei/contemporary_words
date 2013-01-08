require 'erb'

task :build do

  words = Set.new(
    IO.read('contemporary_fiction.txt').split(/\s+/) +
    IO.read('contemporary_poetry.txt').split(/\s+/)
  )
  filtered_words = words.select { |word| word =~ /^[a-z]+$/ }
  sorted_words = filtered_words.sort do |x, y|
    length_compare = x.length <=> y.length
    (length_compare == 0) ? ( x <=> y ) : length_compare
  end

  ruby_code = ERB.new( IO.read "template.erb" )
  Dir.mkdir('lib') unless File.exist? 'lib'
  IO.write('lib/contemporary_words.rb', ruby_code.result(binding))

  sh %{ gem build contemporary_words.gemspec }
end

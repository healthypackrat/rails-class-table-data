require 'json'
require 'pathname'

require 'bundler/setup'

require 'nokogiri'

def char_count(str)
  str.gsub(/\s+/, ' ').strip.size
end

base_dir = Pathname.new(__dir__)

tmp_dir = base_dir.join('tmp')

doc_dir = tmp_dir.join(File.read('RAILS_VERSION').chomp)

task :default => 'entries.json'

file 'entries.json' => 'RAILS_VERSION' do |t|
  entries = doc_dir.glob('classes/**/*.html').map do |html_path|
    entry = {
      class_name: nil,
      path: html_path.relative_path_from(tmp_dir).to_s,
      class_desc: 0,
      method_count: 0,
      method_desc: 0,
      total: 0
    }

    root = Nokogiri::HTML(html_path.read)

    entry[:class_name] = root.at('title').text

    description = root.at('#content > .description')

    if description
      entry[:class_desc] = char_count(description.text)
    end

    methods = root.search('#content > .method > .description')

    entry[:method_count] = methods.size

    entry[:method_desc] = methods.sum {|m| char_count(m.text) }

    entry[:total] = entry[:class_desc] + entry[:method_desc]

    entry
  end

  entries.sort_by! do |entry|
    entry[:class_name]
  end

  File.write(t.name, JSON.pretty_generate(entries))
end

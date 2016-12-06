require "ffi_gen"
require "fileutils"

task default: %w[test]

task :test do
	#puts find_headers("cef")
	run_test(
	  module_name: "CEF",
	  ffi_lib:     "cef",
	  #cflags: 	   ["-nostdinc", "-Iheaders"],
	  cflags: 	   ["-I.", "-Icef", "-I/usr/lib/gcc/x86_64-linux-gnu/5/include", "-I/usr/include/x86_64-linux-gnu", "-I/usr/include"],
	  prefixes:    ["cef_", "_cef_", "CEF_"],
      suffixes:    ["_t"],
	  #files:       find_headers("cef")
	  files:       [
	  				"include/internal/cef_types_linux.h",
	  				"include/internal/cef_types.h",
            "include/internal/cef_string.h",
            "include/internal/cef_string_types.h",
	  				"include/capi/cef_base_capi.h",
            "include/capi/cef_client_capi.h",
            "include/capi/cef_command_line_capi.h",
            "include/capi/cef_browser_process_handler_capi.h",
            "include/capi/cef_app_capi.h",
            "include/capi/cef_browser_capi.h"
	  			   ]
	)
end

def find_headers(dir, prefix = "")
  Dir.chdir dir do
    return Dir.glob("#{prefix}**/*.h")
  end
end

def run_test(options = {})
  output_file = "#{File.dirname(__FILE__)}/output/#{options[:module_name]}.java"
  #options[:files].each do |header|
    #output_file = "#{File.dirname(__FILE__)}/output/#{header.sub(/\.h$/, ".java")}"
    FileUtils.mkdir_p File.dirname(output_file)
    puts "Parsing #{options[:files]}"
    FFIGen.generate(
      module_name: options[:module_name],
      ffi_lib:     options[:ffi_lib],
      headers:     options[:files],
      cflags:      options.fetch(:cflags, []),
      prefixes:    options.fetch(:prefixes, []),
      suffixes:    options.fetch(:suffixes, []),
      blocking:    options.fetch(:blocking, []),
      package:     "cef.capi",
      output:      output_file
    )
  #end
  
  puts "#{options[:module_name]} test successful"
end
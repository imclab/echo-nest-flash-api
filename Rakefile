AS_FILES = FileList["src/**/*.as"]
LIBRARIES = ['lib/as3corelib/bin/as3corelib.swc']

directory 'dist/lib'

file 'dist/lib/echo-nest-flash-api.swc' => AS_FILES + LIBRARIES do
  library_path = LIBRARIES.join(',')
  include_classes = AS_FILES.pathmap("%{^src/,}X")
  puts include_classes

  o = 'dist/lib/echo-nest-flash-api.swc'
  sh "compc -source-path src -include-classes #{include_classes} -library-path+=#{library_path} -o #{o}"
end

task :submodule do
  sh 'git submodule init'
  sh 'git submodule update'
end

file 'lib/as3corelib/build/build.xml' => :submodule

file 'lib/as3corelib/bin/as3corelib.swc' => 'lib/as3corelib/build/build.xml' do
  sh 'cd lib/as3corelib/build && ant'
end

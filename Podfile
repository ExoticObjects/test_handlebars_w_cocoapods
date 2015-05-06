
platform :ios, '7.0'

pod 'handlebars-objc', '~> 1.3.0'

post_install do |installer|

	# Adds the specified compiler flags to the given file in the project.
    #
    # @param [Xcodeproj::Project] project
    #                             The Xcode project instance.
    #
    # @param [String] filename
    #                 The name of the file to work with.
    #
    # @param [String] new_compiler_flags
    #                 The compiler flags to add.
    #
    # @example Disable some warning switches for JSONKit:
    #   add_compiler_flags(installer.project,
    #       "JSONKit.m",
    #       "-Wno-deprecated-objc-isa-usage -Wno-format")
    #
    def add_compiler_flags(project, filename, new_compiler_flags)

        # find all PBXFileReference objects of the given file
        files = project.files().select { |file|
            file.display_name() == filename
        }

		hb_file = files.first

		# puts '*********************project file : ' + project.objects.inspect
		# puts '*********************project native targets : ' + project.native_targets().inspect

		# Gets main debug and release targets
		# puts '*********************project.build_configuration_list() : ' + project.build_configuration_list()
        
        # puts '*********************hb_file.path : ' + hb_file.path + 
        # 							' hb_file.uuid: ' + hb_file.uuid

		project.native_targets().map { |native_target| 

			puts 'native_target: ' + native_target.build_configuration_list().build_configurations.inspect
		}

        # get the PBXBuildFile references of the found files
        # PBXBuildFile actually contains flags for building the file
        build_files = files.map { |file|
            file.build_files()
            puts 'build_file: ' + file.inspect
        }.compact.flatten

        # build_configurations = project.build_configurations().select { |config]
        # 	config.


        # puts '*********************build files : ' + build_files.inspect

        # compiler flags key in settings
        compiler_flags_key = "COMPILER_FLAGS"

        if build_files.length > 0
            build_files.each { |build_file|
                settings = build_file.settings
                if settings.nil?
                    # If we don't have settings for the file we create a new hash
                    settings = Hash[compiler_flags_key, new_compiler_flags]
                else
                    compiler_flags = settings[compiler_flags_key]
                    compiler_flags = (compiler_flags.nil?) ?
                        new_compiler_flags :
                        (compiler_flags + " " + new_compiler_flags)
                    settings[compiler_flags_key] = compiler_flags
                end
                build_file.settings = settings
            }
        else
            puts "No build file refs found for #{filename}!"
        end
    end

    # compiler flags that turn off the JSONKit's warnings
    HANDLEBARS_FLAGS = "-fno-objc-arc -w -Xanalyzer -analyzer-disable-checker -Xanalyzer deadcode"
    add_compiler_flags(installer.project, "Pods-handlebars-objc-Private.xcconfig", HANDLEBARS_FLAGS)
     	
 #  	installer.project.targets.each do |target|

 #  		puts '********************************** target.name: ' + target.name

 #  		if target.name == 'Pods-handlebars-objc'

 #  			# puts '********************************** target.name: ' + target.name

	# 		target.build_configurations.each do |config|

	# 			puts '********************************** config.name: ' + config.name

	# 			config.build_settings['OTHER_CFLAGS'] = '-fno-objc-arc -w -Xanalyzer -analyzer-disable-checker -Xanalyzer deadcode'

	# 		end
 #  		end	    
	# end
end
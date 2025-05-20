#!/usr/bin/env python
from glob import glob
from pathlib import Path
import os

env = SConscript("godot-cpp/SConstruct")

env.Append(CPPPATH=["src/"])
sources = Glob("src/*.cpp")

(extension_path,) = glob("demo/addons/aircraft/*.gdextension")

addon_path = Path(extension_path).parent

project_name = Path(extension_path).stem

scons_cache_path = os.environ.get("SCONS_CACHE")
if scons_cache_path != None:
	CacheDir(scons_cache_path)
	print("Scons cache enabled... (path: '" + scons_cache_path + "')")

if env["target"] in ["editor", "template_debug"]:
	doc_data = env.GodotCPPDocData("src/gen/doc_data.gen.cpp", source=Glob("doc/doc_classes/*.xml"))
	sources.append(doc_data)

debug_or_release = "release" if env["target"] == "template_release" else "debug"
if env["platform"] == "macos":
	library = env.SharedLibrary(
		"{0}/bin/lib{1}.{2}.{3}.framework/{1}.{2}.{3}".format(
			addon_path,
			project_name,
			env["platform"],
			debug_or_release,
		),
		source=sources,
	)
else:
	library = env.SharedLibrary(
		"{}/bin/lib{}.{}.{}.{}{}".format(
			addon_path,
			project_name,
			env["platform"],
			debug_or_release,
			env["arch"],
			env["SHLIBSUFFIX"],
		),
		source=sources,
	)

Default(library)

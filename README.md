Go JavaScript Bindings
======================

Highly experiemental, I'm not even sure these work currently. Original author is Robery Johnstone, and his mercurial repository can be found at https://bitbucket.org/rj/golang-javascriptcore/. I have updated the bindings to work with the latest changes to the reflect API, bits of it manually. The entire test suite minus one function (finally!) passes.

Use
---

Install:
(goinstall doesn't work, likely because of cgo and headers)

	git clone git@github.com:crazy2be/gojs.git
	cd gojs
	gomake install

Import:

	import "gojs"

Use:

	package main

	import (
		"gojs"
		"fmt"
	)

	func main() {
		ctx := gojs.NewContext()
		defer ctx.Release()

		ret, err := ctx.EvaluateScript("['hello', 'world'].join(' ')", nil, ".", 0)

		if err != nil {
			fmt.Println("Script had an error :(", ctx.ToStringOrDie(err))
			return
		}

		if ret == nil {
			fmt.Println("Nothing returned...")
			return
		}

		retstr := ctx.ToStringOrDie(ret)

		fmt.Println(retstr)
	}


Documentation
-------------

There's not much documentation, because the original had no documentation. If I find a use for this beyond curiousity, I might add that as I go. Current documentation generated by godoc is available at http://gopkgdoc.appspot.com/pkg/github.com/crazy2be/gojs.
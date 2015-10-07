
cmake_minimum_required(VERSION 2.8)
project(splitdist)


find_package(BISON)
find_package(FLEX)

BISON_TARGET(MyParser parser.yy ${CMAKE_CURRENT_BINARY_DIR}/parser.cc)
FLEX_TARGET(MyScanner lexer.ll ${CMAKE_CURRENT_BINARY_DIR}/lexer.cc)
ADD_FLEX_BISON_DEPENDENCY(MyScanner MyParser)

add_executable(sdist
               options.hh options.cc
               lexer.cc parser.cc parser.hh
               tree.hh tree.cc visitor.hh visitor.cc
               bitset.hh bitset.cc
               split-set.hh split-set.cc
               label-map.hh label-map.cc
               label-map-visitor.hh
               set-traverser.hh set-traverser.cc
               set-builder.hh set-builder.cc
               set-matcher.hh set-matcher.cc
               split-set-count.hh split-set-count.cc
               sdist.cc)


add_executable(parser_test
               lexer.cc parser.cc parser.hh
               tree.hh tree.cc
               visitor.hh visitor.cc
               parser-test.cc)

#add_executable(visitor_test
#               lexer.cc parser.cc parser.hh
#               tree.hh tree.cc
#               visitor.hh visitor.cc
#               visitor-test.cc)

add_executable(bitset_test
               bitset.hh bitset.cc
               bitset-test.cc)

add_executable(split_set_test
               bitset.hh bitset.cc
               label-map.hh label-map.cc
               split-set.hh split-set.cc
               split-set-test.cc)

add_executable(label_map_test
              label-map.hh label-map.cc
              label-map-test.cc)

add_executable(label_map_visitor_test
               lexer.cc parser.cc parser.hh
               tree.hh tree.cc
               visitor.hh visitor.cc
               label-map.hh label-map.cc
               label-map-visitor.hh 
               label-map-visitor-test.cc)

add_executable(set_builder_test
               lexer.cc parser.cc parser.hh
               tree.hh tree.cc visitor.hh visitor.cc
               bitset.hh bitset.cc
               label-map.hh label-map.cc
               label-map-visitor.hh 
               set-traverser.hh set-traverser.cc
               split-set.hh split-set.cc 
               split-set-count.hh split-set-count.cc 
               set-builder.hh set-builder.cc
               set-builder-test.cc)

#add_executable(set_matcher_test
#               lexer.cc parser.cc parser.hh
#               tree.hh tree.cc visitor.hh visitor.cc
#               bitset.hh bitset.cc
#               label-map.hh label-map.cc
#               label-map-visitor.hh 
#               set-traverser.hh set-traverser.cc
#               set-builder.hh set-builder.cc
#               split-set.hh split-set.cc 
#               split-set-count.hh split-set-count.cc
#               options.hh options.cc
#               set-matcher.hh set-matcher.cc
#               set-matcher-test.cc)

enable_testing()
add_test(ParserTest parser_test)
#add_test(VisitorTest visitor_test)
add_test(BitSetTest bitset_test)
add_test(SplitSetTest split_set_test)
add_test(LabelMapTest label_map_test)
add_test(LabelMapVisitorTest label_map_visitor_test)
add_test(SetBuilderTest set_builder_test)
#add_test(SetMatcherTest set_matcher_test)

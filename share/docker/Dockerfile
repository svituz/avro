# Licensed to the Apache Software Foundation (ASF) under one
# or more contributor license agreements.  See the NOTICE file
# distributed with this work for additional information
# regarding copyright ownership.  The ASF licenses this file
# to you under the Apache License, Version 2.0 (the
# "License"); you may not use this file except in compliance
# with the License.  You may obtain a copy of the License at
#
#     http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

# Dockerfile for installing the necessary dependencies for building Avro.
# See BUILD.txt.

FROM dockerfile/java:openjdk-7-jdk

WORKDIR /root

# Install dependencies from packages
RUN apt-get update && apt-get install --no-install-recommends -y \
  git subversion curl ant make maven \
  gcc cmake asciidoc source-highlight \
  g++ flex bison libboost-all-dev doxygen \
  mono-devel mono-gmcs nunit \
  nodejs nodejs-legacy npm \
  perl \
  php5 phpunit php5-gmp \
  python python-setuptools python3-setuptools \
  ruby ruby-dev rake

# Install Forrest
RUN mkdir -p /usr/local/apache-forrest
RUN curl -O http://archive.apache.org/dist/forrest/0.8/apache-forrest-0.8.tar.gz
RUN tar xzf *forrest* --strip-components 1 -C /usr/local/apache-forrest
RUN echo 'forrest.home=/usr/local/apache-forrest' > build.properties

# Install Perl modules
RUN curl -L http://cpanmin.us | perl - --self-upgrade # non-interactive cpan
RUN cpanm install Module::Install Module::Install::ReadmeFromPod \
  Module::Install::Repository \
  Math::BigInt JSON::XS Try::Tiny Regexp::Common Encode \
  IO::String Object::Tiny Compress::Zlib Test::More \
  Test::Exception Test::Pod

# Install Ruby modules
RUN gem install echoe yajl-ruby multi_json

# Install global Node modules
RUN npm install -g grunt-cli

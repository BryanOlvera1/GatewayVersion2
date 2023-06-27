# GatewayVersion2
html/css restaurant site



package com.example.capstone.controllers;

import com.example.capstone.Model.AccountType;
import com.example.capstone.Model.Agency;
import com.example.capstone.dataAccess.IAgencyRepo;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.http.HttpStatus;
import org.springframework.http.ResponseEntity;
import org.springframework.web.bind.annotation.CrossOrigin;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.PathVariable;
import org.springframework.web.bind.annotation.RestController;

import java.util.Optional;

@RestController
@CrossOrigin
public class AgencyController {

    @Autowired
    private IAgencyRepo agencyRepo;

    @GetMapping("/agency")
    public Iterable<Agency> getAgency(){return agencyRepo.findAll();}

    @GetMapping("/agency/{id}")
    public ResponseEntity<?> getAgencyById(@PathVariable("id") Long id) {
        Optional<Agency> AgencyOptional = agencyRepo.findById(id);
        if (AgencyOptional .isPresent()) {
            Agency Agency1 = AgencyOptional.get();
            return ResponseEntity.ok(Agency1);
        } else {
            return ResponseEntity.status(HttpStatus.NOT_FOUND).body("Account not found with ID: " + id);
        }
    }

    @Autowired
    public void setAgencyRepo(IAgencyRepo agencyRepo){
        this.agencyRepo = agencyRepo;
    }
}

###
package com.example.capstone.dataAccess;


import com.example.capstone.Model.Agency;
import org.springframework.data.repository.CrudRepository;
import org.springframework.stereotype.Repository;


@Repository
public interface IAgencyRepo  extends CrudRepository<Agency, Long> {

}
####
package com.example.capstone.Model;

import javax.persistence.*;

@Entity
@Table(name = "Agency")
public class Agency {
    @Id
    @GeneratedValue

    @Column(name = "id")
    private Long id;
    @Column(name = "name")
    private String name;


    @Column(name = "ein")
    private String ein;
    @Column(name = "address1")
    private String  address1;

    @Column(name = "address2")
    private String address2;
    @Column(name = "city")
    private String city;
    @Column(name = "st")
    private String st;
    @Column(name = "zip")
    private String zip;
    @Column(name = "desc")
    private String desc;

    public Long getId() {
        return id;
    }

    public void setId(Long id) {
        this.id = id;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public String getEin() {
        return ein;
    }

    public void setEin(String ein) {
        this.ein = ein;
    }

    public String getAddress1() {
        return address1;
    }

    public void setAddress1(String address1) {
        this.address1 = address1;
    }

    public String getAddress2() {
        return address2;
    }

    public void setAddress2(String address2) {
        this.address2 = address2;
    }

    public String getCity() {
        return city;
    }

    public void setCity(String city) {
        this.city = city;
    }

    public String getSt() {
        return st;
    }

    public void setSt(String st) {
        this.st = st;
    }

    public String getZip() {
        return zip;
    }

    public void setZip(String zip) {
        this.zip = zip;
    }

    public String getDesc() {
        return desc;
    }

    public void setDesc(String desc) {
        this.desc = desc;
    }
}
##
package com.example.capstone.services;

import com.example.capstone.Model.Agency;
import com.example.capstone.dataAccess.IAgencyRepo;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;

@Service
public class AgencyService implements IAgencyService {
    IAgencyRepo agencyRepo;

    @Override
    public Iterable<Agency> getAgency(){ return agencyRepo.findAll(); }

    public IAgencyRepo getAgencyRepo() {
        return agencyRepo;
    }
    @Autowired
    public void setAgencyRepo(IAgencyRepo agencyRepo){
        this.agencyRepo = agencyRepo;
    }
}

###
package com.example.capstone.services;

import com.example.capstone.Model.Agency;

public interface IAgencyService {

    Iterable<Agency> getAgency();
}

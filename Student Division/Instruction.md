# Instruction

**Note: Every file is also available at [here](https://drive.google.com/drive/folders/11AjL3dAiu_29xmRoZeGlTmtme_W388tG?usp=sharing) and trained on GPU `Colab Pro` version. In progress, since we don't set seed, every result that is generated again by yourself is approximate, not exact 100% with below results.
Sometimes, you need more phases or epochs to get the result. Good luck!**

To get this final result in the contest, I trained on MEGNet Model through 5 phases.

```buildoutcfg

    train, test = train_test_split(data, test_size=0.33, random_state=666)
    
    model = MEGNetModel(
            graph_converter=CrystalGraph(cutoff=r_cutoff),
            centers=gaussian_centers,
            width=gaussian_width,
            embedding_dim=32,
            nblocks=5,
            loss=["MAE"],
            npass=2,
            lr=lr,
            metrics=energy_within_threshold,
        )
        
    model.train(
        train.structures,
        train.targets,
        validation_structures=test.structures,
        validation_targets=test.targets,
        epochs=int(config["model"]["epochs"]),
        batch_size=int(config["model"]["batch_size"]),
        # prev_model= (see below)
        save_checkpoint=True,
    )
```

## Phase 1
```buildoutcfg
    epochs = 1000
    batch_size = 128
    lr = 1e-3
    cutoff = 4
    
    prev_model = None
```

At the end of the phase, we can get a file continuing to train model for next phase as `val_mae_00918_0.037034.hdf5` and
`energy_within_threshold` is approximately `0.65`. Callback of this phase was not saved by ourselves, I am so sorry to each reader. 

## Phase 2
```buildoutcfg
    epochs = 1500
    batch_size = 128
    lr = 1e-4
    cutoff = 4
    
    prev_model = 'val_mae_00918_0.037034.hdf5'
```

At the end of the phase, we can get a file continuing to train model for next phase as `val_mae_01407_0.018234.hdf5` and 
`energy_within_threshold` is approximately `0.75`. Callback of this phase is [here](https://drive.google.com/drive/folders/1psBgx2lPr8F1SwKGJYJ9kvnmc3gFk7Vj?usp=sharing).

## Phase 3
```buildoutcfg
    epochs = 1500
    batch_size = 128
    lr = 1e-4
    cutoff = 4
    
    prev_model = 'val_mae_01407_0.018234.hdf5'
```

At the end of the phase, we can get a file continuing to train model for next phase as `val_mae_01383_0.017545.hdf5` and
`energy_within_threshold` is approximately `0.79`. Callback of this phase is [here](https://drive.google.com/drive/folders/1mV6A3SXCd3Kg_IxYH9Rw7XQK1lkOIvXz?usp=sharing).


## Phase 4
```buildoutcfg
    epochs = 1500
    batch_size = 128
    lr = 1e-4
    cutoff = 4
    
    prev_model = 'val_mae_01383_0.017545.hdf5'
```

At the end of the phase, we can get a file continuing to train model for next phase as `val_mae_01700_0.008908.hdf5` and
`energy_within_threshold` is approximately `0.85`. Callback of this phase is [here](https://drive.google.com/drive/folders/1VzmX3VcS2yOkDvCxdM_wtaqmB5o1-vb0?usp=sharing).


## Phase 5
```buildoutcfg
    epochs = 2000
    batch_size = 128
    lr = 1e-4
    cutoff = 4
    
    prev_model = 'val_mae_01700_0.008908.hdf5'
```

At the end of the phase, we can get a file continuing to train model for next phase as `val_mae_01407_0.018234.hdf5` and
`energy_within_threshold` is approximately `0.92`. Callback of this phase is [here](https://drive.google.com/drive/folders/1JQyu23kYSk626zFoPPNhrb3dLI-vt7jx?usp=sharing).
